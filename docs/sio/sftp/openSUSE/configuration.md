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

Je vais tester la connexion au sftp 

### Par ligne de commande

![sftp cli](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/sftp_cli.png)

La connexion en sftp fonctionne d'où le shell "sftp>"

### Avec FileZilla

![sftp filezilla](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/sftp_filezilla.png "sftp filezilla")

je me connecte comme pour un FTP mais j'entre le port 22. Ainsi je n'ai pas besoin de créer un certificat.

Il m'est proposé par défaut.

Et je retrouve mon fichier texte sans bouger de répertoire donc je suis dans mon répertoire racine /srv/sftp/

![sftp filezilla 2](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/sftp_filezilla_2.png "sftp filezilla 2")

Le répertoire racine est bien /srv/sftp avec mon fihier texte

 
