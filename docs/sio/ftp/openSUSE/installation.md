# Installation sur OpenSUSE

## Installer vsftpd

On utilisera le logiciel ftp "vsftpd" pour very secure ftp daemon.
Il est déjà installé de base. Vérifier avec la commande `zypper info vsftpd`

* Sinon l'installer avec `sudo zypper install vsftpd`

Ou via "installer et supprimer des logiciels de Yast"

* Cocher l'appli 
* Cliquer sur accepter

![Installer vsftpd yast](https://github.com/1Tyron140/doc/raw/main/images/ftp/yast_ftp.png)

## Installer l'outil Yast pour gérer le ftp

L'installation va se faire par interface graphique avec l'outil d'administration intégré à OpenSUSE: Yast.
Il faut installer la fonctionnalité permettant de gérer le ftp avec Yast

`sudo zypper install yast2-ftp-server`


![Menu yast ftp](https://github.com/1Tyron140/doc/raw/main/images/ftp/ftp_general_yast.png)

L'interface graphique revient à éditer le fichier `/etc/vsftpd.conf`
