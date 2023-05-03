# Configuration du serveur SFTP sur Debian 11

En root

## SSH

### Autoriser seulement les utilisateurs authentifiés

* Dans `/etc/ssh/sshd_config`

* Ajouter en fin de fichier `PasswordAuthentication Yes`
* `AllowUsers User` remplacer user par l'utilisateur voulu
ou
* 'AllowGroups group' et remplacer par le groupe voulu

## Test de connexion 

Avec Filezilla, WinSCP ou un autre client ftp