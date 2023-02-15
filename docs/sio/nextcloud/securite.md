# Amélioration de la sécurité

## Fail2ban

La plateforme nextcloud peut être hébergée en interne ou ouverte à l'extérieur. Dans les deux cas elle peut être sujette à des attaques par force brute. Cependant elle intègre une fonction de protection contre cette attaque. 

### Attaque par force brute

Je vais mener une attaque par force brute pour sur ma plateforme en localhost sur un compte crée pour l'occasion afin de montrer que l'attaque par force brute n'est pas interrompue.
<br>`Login: test_brute`
avec la commande:
```
$ hydra -V -f -l test_brute -P rockyou.txt -s 80 http-get://localhost/nextcloud/index.php/login
```
Sur cette image on voit que ma tentative a été interceptée au bout de 16 tentatives
![tenative_hydra](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/hydra.jpg "tentative brute force")


Le serveur a renvoyé un mauvais mot de passe comme mot de passe valide pour bloquer l'attaque.

Dans cette table on voit le journal des attaques:
![tenative_hydra](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/bruteforce_attempts.jpg "table bruteforce")

et on ne peut plus se connecter:
![tenative_hydra](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/connexion_refusee.jpg "accès bloqué")
La commande `sudo -u wwwrun php /srv/www/htdocs/nextcloud/occ security:bruteforce:reset <adresse ip>`
### Qu'est ce que fail2ban

On peut installer fail2ban pour renforcer cette sécurité. Cette outil opensource va venir bloquer une adresse ip grâce à iptables selon certaines conditions (exemple: 5 tentatives échouées). 

### Installation

On ajoute le dépôt d'abord pour pouvoir récupérer le paquet:
```
sudo zypper addrepo https://download.opensuse.org/repositories/security/openSUSE_Leap_15.3_Update/security.repo
sudo zypper refresh
sudo zypper install fail2ban
```
Et l'activer: `sudo systemctl enable fail2ban.serice --now`
### Création d'un filtre et d'une prison

__Les filtres__ servent à définir les cas qui activeront la prison, ici: les cas d'échecs d'authentification.

Dans `/etc/fail2ban/filter.d/` il y a plein d'autre filtres comme `nagios.conf` ou `bitwarden.conf` alors on crée nextcloud.conf dans le repertoire: `sudo nano nextcloud.conf`.

Et coller ces lignes de regex: 
```
[Definition]
_groupsre = (?:(?:,?\s*"\w+":(?:"[^"]+"|\w+))*)
failregex = ^\{%(_groupsre)s,?\s*"remoteAddr":"<HOST>"%(_groupsre)s,?\s*"message":"Login failed:
datepattern = ,?\s*"time"\s*:\s*"%%Y-%%m-%%d[T ]%%H:%%M:%%S(%%z)?"
```

__Les prisons__ (ou jail) sont les punitions qui vont être appliquées, comme un bannissement de 50000 secondes.

Dans `/etc/fail2ban/jail.d/`, créer `nextcloud.local` avec ce contenu:

```
[nextcloud]
backend = auto
enabled = true
port = 80,443
protocol = tcp
filter = nextcloud
maxretry = 5
bantime = 86400
findtime = 43200
logpath = /srv/www/htdocs/nextcloud/data/nextcloud.log
```
On lit qu'au bout de 5 tentatives, un ban de 86400 secondes (24 heures) est appliqué.

Relancer le service : `sudo systemctl restart fail2ban.service`

Ensuite la commande `fail2ban-client status` nous affiche les prisons activées:

```
Status
|- Number of jail:    1
 - jail list: nextcloud
```
Après quelques tentatives échouées, les logs de fail2ban montrent que les filtres foncitonnent correctemen, mais a été ignorée car il s'agit des requêtes du serveur.

![image log fail2ban](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/fail2ban_log.jpg)

## Utiliser HTTPS (auto-signé)

Pour ne pas que les mots de passe ou autres informations circulent en clair, je vais activer le protocole HTTPS àl'aide de certificat auto-signés. Il n'y a pas de soucis puisque le serveur est en local.

Le site est en local alors je ne pourrais pas utiliser certbot.

Pour cela j'aurais besoin de openssl (devrait déjà être installé) et de l'accès root.

`zypper install openssl `

### Création des certificats

`openssl req -newkey rsa:4096 -x509 -days 365 -nodes -keyout /etc/apache2/ssl.key/macle.key -out /etc/apache/ssl.crt/moncert.crt`

Saisir les informations souhaitées ensuite, exemple:
```
Country Name (2 letter code) [US]:FR
State or Province Name (full name) [Some-State]:
Locality Name (eg, city) []:
Organization Name (eg, company) [Internet Widgits Pty Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:localhost
Email Address []:
```

### Activation des modules nécessaires

```
a2enmod ssl
a2enmod socache_shmcb
```

Et redémarrer le service apache2

### Activation de SSL/TLS

* Aller dans `/etc/apache2/vhosts.d`
* Copier `vhost-ssl.template` vers `vhost-ssl-nextcloud.conf`
* Mettre le bon chemin racine après DocumentRoot: `/srv/www/htdocs/nextcloud`
* Mettre le nom du site après ServerName: `localhost`
* Mettre le bon chemin du certificat `SSLCertificateFile /etc/apache2/ssl.key/<votre certificat>`
* Mettre le bon chemin de la clé `SSLCertificateKeyFile /etc/apache/ssl.crt/<votre clé>`
* Ouvrir `/etc/sysconfig/apache2` et chercher `APACHE_SERVER_FLAGS=""`, y ajouter SSL dans les guillemets
* Sauvegarder et redémarrer le service apache2


Sur `https//127.0.0.1`, la connexion est "non sécurisée" car c'est moi-même qui la signé et non une autorité de certification, mais la page et en https.
![image https nextcloud](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/nextcloud_https_1.jpg)

Le protocole TLS est activé:
![image https nextcloud](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/page_chiffree.jpg)

### Redirection http vers https

Dans le fichier /etc/apache2/conf.d/nextcloud.conf, ajouter:
```
<VirtualHost *:80>
   ServerName localhost
   Redirect permanent / https://localhost
</VirtualHost>
```
## Mise à jour de nextcloud

### Erreur de mise à jour
Lors de l'accès à la page nextcloud, il est proposé de mettre à jour le serveur.


![page de mise à jour](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/demarrer_maj.png)

On clique sur démarrer

![erreur de mise à jour auto](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/erreur_maj_skip_version.png)

Une erreur se produit.

Le serveur est en version 21.x.y et il est indiqué qu'il passera en version 23.0.5. Une version a donc été sautée ce qui provoque des erreurs.

D'après la [documentation](https://docs.nextcloud.com/server/latest/admin_manual/maintenance/upgrade.html#:~:text=You%20cannot%20skip,18.0.11%20%2D%3E%2019.0.5%20%2D%3E%2020.0.2):

```
* Vous ne pouvez pas sauter des versions majeures. Veuillez réexécuter la mise à niveau jusqu'à ce que vous ayez atteint la dernière version disponible (ou applicable)..

* Exemple: 18.0.5 -> 18.0.11 -> 19.0.5 -> 20.0.2
```

En ouvrant le ficier `config.php`: `sudo nano /srv/www/htdocs/nextcloud/config/config.php`
Je lis que nextcloud est en version 21.0.9.1, la lus récente de la version 21. Alors on peut passer à la suivante, soit la 22.2.10. 

### Mise à jour manuelle

On passe le serveur en mode maintenance

 (en root): `sudo -u wwwrun php /srv/www/htdocs/nextcloud/occ maintenance:mode --on`

>Si la commande 'php' est introuvable
>
>Installer le paquet php-cli

* On arrête le serveur web

`sudo systemctl stop apache`

* Copie des répertoires /config et /data (facultatif)

    * On peut les sauvegarder où l'on veut, personnellement j'ai crée un répertoire /srv/backup/nextcloud/:

`sudo cp -r /srv/www/htdocs/nextcloud/data data`

`sudo cp -r /srv/www/htdocs/nextcloud/config config`

* Renommer le repertoire nextcloud actuel en /old-nextcloud

`sudo mv /srv/www/htdocs/nextcloud /srv/www/htdocs/old-nextcloud`

* Télécharger l'archive de la version 22.2.10

    * En téléchargant directement sur [la page nextcloud changelog](https://download.nextcloud.com/server/releases/nextcloud-22.2.10.zip)
    * Avec wget : `sudo wget https://download.nextcloud.com/server/releases/nextcloud-22.2.10.zip`

* Déplacer l'archive dans le repertoire nextcloud

`sudo mv /chemin/vers/nextcloud-22.2.10.zip /srv/www/htdocs/nextcloud-22.2.10.zip`

* Décompresser 

`sudo unzip nextcloud-22.2.10.zip`

*  Copie des repertoires config et data vers le nouveau repertoier nextcloud
`sudo unalias cp` permet de retirer les alias de cp comme "cp -i" qui demande une confirmation pour chaque fichier, cela peut être remis ensuite

`sudo cp -r /srv/www/htdocs/old-nextcloud/config/ /srv/www/htdocs/nextcloud/ `

`sudo cp -r /srv/www/htdocs/old-nextcloud/data/ /srv/www/htdocs/nextcloud/ `

* Mettre le compte web en propriétaire 

` sudo chown -R wwwrun:www /srv/www/htdocs/nextcloud/`

* Changer les droits 
    * Sur les repertoires `sudo find nextcloud/ -type d -exec chmod 750 {} \;`
    * Sur les fichiers `sudo find nextcloud/ -type f -exec chmod 640 {} \;`
    
> La commande (en root) `sudo -u wwwrun php /srv/www/htdocs/nextcloud/occ -V` nous renvoie la version"22.2.10"

* Redémarrer le serveur apache

* Mise à niveau

Dans le repertoire nextcloud:

`sudo -u wwwrun php occ upgrade`

![Nouvelle maj installée](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/maj_faite.png)

La mise à jour a abouti

![menus après maj](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/menu_apres_maj.png)

Tout est comme avant

* On peut maintenant supprimer le zip, le repertoire old-nextcloud, sortir du mode maintenance et répeter la procédure jusqu'à la version souhaitée !

>Note pour moi même
>
> Mise à jour faite en 07:18.82

## Gestion des droits

Dans nextcloud on peut modifier les droits des fichiers et des dossiers pour assurer la confidentialité.
On va créer un dossier "maintenance", et le rendre accessible uniquement aux personnes concernées grâce aux habilitatiions.

Sur le compte admin, on peut créer des utilisateurs et des groupes.

* Aller dans le menu d'administration des utilisateurs

![menu](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/menu_users.png)

* Créer un groupe en cliquant sur "ajouter un groupe"

![menu](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/creer_groupe.png)

* Créer un dossier dans l'accueil

![menu](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/nvo_dossier.png)

* Ajouter le groupe "Maintenance" à la liste de droits en cliquant sur le logo partage

![menu](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/partage_groupe.png)

* Voici la liste de droits

![menu](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/droits.png)

* Ajouter des utilisateur au groupe Maintenance, valider

![menu](https://github.com/1Tyron140/doc/raw/main/images/nextcloud/ajout_user_groupe.png)
