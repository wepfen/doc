# Configuration 
en root ou avec sudo 


## Groupes et utilisateurs

* Créer un groupe pour les utilisateurs autorisés à ce connecter au SFTP:

    * En ligne de commande `groupadd sftpusers` 
    * Avec Yast `Yast > Sécurité et utilisateurs > groupe > ajouter`

* Ajouter les utilisateurs à ce groupe:

    * En interface graphique avec yast `Yast > Sécurité et utilisateurs > groupe > sftpusers > cocher les users et valider"`
    * En ligne de commande `usermod -aG user sftpusers`

## SSH

On aura besoin de modifier le fichier  `/etc/ssh/sshd_config`

* L'ouvrir: `nano /etc/ssh/sshd_config`


### Répertoire racine

* En fin de fichier, commenter la ligne `Subsystem  sftp    /usr/lib64/ssh/sftp-server` avec un '#' en début de ligne

* Écrire juste en dessous `Subsystem sftp internal-sftp`, cela permet de faire fonctionner chroot permettant dfe choisir le répertoire racine.

* Création du répertoire racine 
```
mkdir /srv/sftp
chown root:sftpusers /srv/sftp
chmod 750 /srv/sftp
```

* Ajouter les règle suivantes dans  `sshd_config`, rajouter tout en bas du  fichier près de l'exemple

```
Match group sftpusers
   ForceCommand internal-sftp
   ChrootDirectory /srv/sftp
   X11Forwarding no
   AllowTcpForwarding no
```
Il est possible de remplacer /srv/ftp par /home/%u pour que chaque utilisateur ait sa racine dans son répertoire personnel.

### Authentification 

* Décommenter "PasswordAuthentication yes" à la ligne 57

* Relancer le serveur à chaque changement de cnfiguration `systemctl restart sshd`

## Test