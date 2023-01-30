# Configuration
## MariaDB

* __S'il s'agit de la première  connexion à la base de donnée, il faudra activer mariadb au démarrage :__
```
systemctl enable mariadb.service --now      #en root
```
* --now pour activer le service, sinon il aurait fallu ajouter `systemctl start mariadb.service`

* __Et lancer l'installation sécurisée__ :
```
mysql_secure_install        #en root
``` 
    * Entrez le mot de passe root actuel (aucun), faire entrée
    * `Switch to unix_socket authentication  [Y/n] n`
    * `Change the root password [Y/n] y` votre_nouveau_mdp_root
    * `Remove anonymous users? [Y/n] y` 
    * `Disallow root login remotely? [Y/n] y`
    * `Remove test database and access to it [Y/n] y`
    * `Reload privilege table [Y/n] y`

* __Et dans tous les cas, configurer MariaDB pour Nextcloud:__
    * __Connexion à la base__ `mariadb -u root -p` avec  `-u` pour utiliser l'user `root` et `-p` pour indiquer qu'on va entrer un mot de passe
    * `create database nextcloud;` __création de la base de donnée nextcloud__
    * `create user nextclouduser@localhost identified by 'mdp_a_definir';`__creation de l'user nextcloud avec son mot de passe qui gérera le base nextcloud__
    * `grant all privileges on nextcloud.* to nextclouduser@localhost identified by 'some-password-here';` __attribution des droits à nextclouduser sur la base de donnée nextcloud__
    * on quitte `exit;`
    * Les login, mot de passe et nom de base de donnée peuvent être définis comme bo vous semble.
    
## Apache
* Activation de modules complémentaires
```
a2enmod php7
a2enmod rewrite
a2enmod headers
a2enmod env
a2enmod dir
a2enmod mime
```
* Activation du service web:
```
systemctl enable apache.service --now      #en root
```

Enfin le serveur peut être accessible à partir de ceraines adresses seulement renseignées dans `/srv/www/htdocs/nextcloud/config/config.php` comme suit
```
'trusted_domains' =>
  array (
   0 => 'localhost',
   1 => 'server1.example.com',
   2 => 'X.X.X.X',
),
```

## PHP 

* Il faut modifier certaines valeurs de php.ini pour nextcloud 
`sudo nano /etc/php7/apache2/php.ini`

```
post_max_size = 50G
upload_max_filesize = 25G
max_file_uploads = 200
max_input_time = 3600
max_execution_time = 3600
session.gc_maxlifetime = 3600
memory_limit = 512M
```

Cependant il est possible d'ajuster les valeurs à votre uilisation et par exemple réduire `upload_max_filesize` à 10Go pour limiter le taille max d'upload d'un fichier.

## Nextcloud

* __Désigner l'utilisateur wwwrun en tant que propriétaire du repertoire nextcloud (en root) :__
```
chown -R wwwrun:wwwrun /srv/www/htdocs/nextcloud/
```
sur debian: `chown -R www-data:www-data /var/www/html/nextcloud/`

* __Sur le réseau de la machine, se connecter sur un navigateur sur `http://<ip de la machine>/nextcloud/`__
![interface nextcloud.](https://raw.githubusercontent.com/1Tyron140/doc/main/images/nextcloud/web-1.jpg)

* __Saisir les informations__
    * Chosir les logins admin pour next cloud
    * Choisir la base mariaDB
    * Saisir les informations pour la base de donnée
![interface nextcloud.](https://raw.githubusercontent.com/1Tyron140/doc/main/images/nextcloud/web-2.jpg)

