# Création des règles de pare-feu sur pfsense

## Résumé du fonctionnement des règles

### Stateful
pFsense est un pare-feu qui fonctionne **avec état** autrement dit **stateful** ce qui signifie qu'il se souvient des flux autorisés pour ensuite en accepter la réponse. 

### Default deny
De plus, pFsense fonctionne en mode **refuser par défaut** ou **Default deny**, tous les flux seront rejetés sauf si une règle créee l'autorise.
Alors pour accéder à internet il faudra autoriser les les flux vers les ports **HTTP/HTTPS et DNS**.

### Filtrage
Enfin les règles filtrent les flux entrants,  c'est à dire que si on veut autoriser le flux LAN vers internet en HTTPS, je me pace sur l'interface LAN et j'ajoute une règle **autoriser le trafic lan vers n'importe quel destinataire vers le port 443**.
Automatiquement, les flux en réponse à cette règle seront acceptés qu'on appelle **quadruplet inversé**, c'est-à-dire un **flux de n'importe quelle adresse d'origine port 443 et destination du LAN**

Plus d'informations sur le [fonctionnement de pFsense](https://docs.netgate.com/pfsense/en/latest/firewall/rule-methodology.html)

## Création des règles 

### Internet depuis le LAN

#### HTTPS

Pour montrer un exemple de confiuration des règles, je vais ajouter les rèles permettant de accéder aux sites internet.

Pour cela il faudra autoriser le flux vers les ports 80 (HTTP), 443 (HTTPS), 53 (DNS) depuis le LAN.

Sur pFsense **pare-feu > règles > LAN > Add**

![règles https](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/rule_https_lan.PNG)
![règles https](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/rule_https_lan_2.PNG)

En résumé, j'**autorise** pour l'nterface **LAN**, en **IPV4** et sur **TCP**  le **trafic du LAN** vers partout (**any**) sur le port de destination **443 (HTTPS)** et j'active la journalisation pour cette règles.

Donc en autorisant le trafic sortant vers HTTPS, la réponse à ce trafic sera autorisée alors qu'avant elles étaient refusée à cause de la politique **Default Deny**.

Cependant internet n'est pas encore accessible car il faut aussi activer le DNS et eventuellement HTTP si l'on veut.

#### DNS 

Pour le flux DNS c'est le même principe, la règle en une ligne

![règles http, https, dns](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/rules_lan_http_dns.PNG)

On peut désormais tester

#### Test 

Je vérifie la connexion d'une machine du LAN vers un site internet

![test connexion LAN vers internet](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/lan_vers_internet.PNG)

Je peux acccéder au site alors ca fonctionne.

### LAN vers DMZ

Dans la zone démillitarisée on retrouve un serveur WEB et un serveur SFTP (un FTP sécurisé via ssh), accessible depuis le LAN et en théorie ouvert à internet. 

Certains flux sont authorisés vers la DMZ cependant le LAN n'acceptera pas les flux inités par une machine de la DMZ afin de sécuriser le LAN de visiteurs extérieurs au réseau.

![schéma des flux du réseau](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/diagramme_deploiement.png)
Tout d'abord on va bloquer le trafic venant de la dmz

* **Pare-feu > règles > LAN > ajouter**
* Bloquer la source DMZ et tous les ports source vers le destinataire LAN vers tous les ports
* S'il le faut, faire glisser la règle en dessous de celles autorisant le trafic afin de ne pas bloquer les requêtes initiées par le LAN

l'ordre des champs su l'image est le suivant: protocole, adresse source, port source, adresse de destination, port de destination, queue, schedule, decription.

![ règles DMZ vers LAN](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/rules_lan_dmz.PNG)



HTTPS / HTTP

* Sur la DMZ on va autoriser le trafic HTTPS/HTTP entrant
* Sur le LAN, rien à faire puisqu'une règle autorisant à se connecter à un port HTTPS/HTTP a déjà été mise en place
* **Pare-feu > règles > DMZ > ajouter**
* Ajouter les règles suivantes:

![regles DMZ entrant HTTPS](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/rules_vers_dmz.PNG)


### DMZ vers internet
