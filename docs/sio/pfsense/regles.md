# Création des règles de pare-feu sur pfsense

## Résumé du fonctionnement des règles

### Stateful
pFsense est un pare-feu qui fonctionne **avec état** autrement dit **stateful** ce qui signifie qu'il se souvient des flux autorisés pour ensuite en accepter la réponse. 

### Default deny
De plus, pFsense fonctionne en mode **refuser par défaut** ou **Default deny**, tous les flux seront rejetés sauf si une règle créee l'autorise.
Alors pour accéder à internet il faudra autoriser les les flux vers les ports **HTTP/HTTPS et DNS**.

### Filtrage
Enfin les règles filtrent les flux entrants,  c'est à dire que si on veut autoriser le flux LAN vers internet en HTTPS, je me pace sur l'interface LAN et j'ajoute une règle **autoriser le trafic lan vers n'importe quel destinataire vers le port 443**.
Automatiquement, les flux en réponse à cette règle seront acceptés, c'est-à-dire un **flux de n'importe quelle adresse d'origine port 443 et destination du LAN**

Plus d'informations sur le [fonctionnement de pFsense](https://docs.netgate.com/pfsense/en/latest/firewall/rule-methodology.html)

