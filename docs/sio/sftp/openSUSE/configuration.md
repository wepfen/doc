## Capture avec wireshark 

On va tester avec wireshark voir si la communication est chiffrée ou non

### Installation

`zypper install wireshark`

* Lancer le programme en étant en root sinon les interfaces intéressantes seront indisponibles

* Sans root

![Wireshark sans privileges](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/wireshark_no_root.png "wireshark sans privilèges")

* Avec root 

![Wireshark avec privileges](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/wireshark_root.png "wireshark avec privilèges")


#### Autoriser un utilisateur non-root à avoir toutes les interfaces

en root,

* Ajouter l'utilisateur souhaité au groupe wireshark

`usermod -aG wireshark user`

* S'assurer que le groupe wireshark puisse exécuter le binaire dumpcap, sinon faire:

`chmod g+x /usr/bin/dumpcap`

Si les changements ne s'appliquent pas, se déconnecter et se reconnecter

### Capture

la capture va s'effectuer avec l'interface "any"

* Lancer la capture

* Se connecter au SFTP 

* Filtrer la capture par ssh en tapant "ssh" puis entrer dans la barre de filtre

On peut voir que je me suis connecté au sftp avec Filezilla

![Wireshark avec privileges](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/wireshark_filezilla.png "connecté avec filezilla")

Et le contenu de ce paquet et de tous les autres est chiffré

![paquet chiffré](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/contenu_chiffré.png "Le contenu est bien chiffré")

## Gestion des habilitations 

Il est possible de gérer les droits pour les différents dossiers et fichiers au sein du répertoire sftp.

### Autoriser l'accès à un groupe

En root

On souhaaite par exemple autoriser l'accès au dossier RH seulement aux membres du groupe RH

* Dans le répertoire racine du sftp, créer le dossier rh

`mkdir rh`

* Créer le groupe rh 

`groupadd rh`

* Mettre le groupe rh en propriétaire du dossier

`chown root:rh rh/`

* Accorder tous les droits au groupe rh et et les retirer aux autres utilisateurs

`chmod 770 rh/`

Je vais mettre le compte 'pcohen' dans le groupe rh et laisser les autres en dehors pour faire la démonstration.

`uermod -aG rh pcohen`

__Avec un compte dans le groupe rh__

Le contenu du dossier a été affiché avec succès et l'utilisateur peut créer des fichiers et les lire

![acces dossier rh](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/filezilla_acces_rh.png "Accès au dossier RH")


__Avec un compte n'appartenant pas au groupe rh__


L'utilisateur ne peut pas accéder au dossier

![refus d'acces dossier rh](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/filezilla_acces_rh_refus.png "Refus d'accès au dossier RH")

### Autoriser l'accès à un utilisateur

* Créer un dossier dans /srv/sftp

`mkdir pcohen`

* Rendre l'utilisateur voulu propriétaire

`chown pcohen /srv/sftp/pcoohen`

* Accorder les droits seulement à l'utilisateur

`chmod 700 /sv/sftp/pcohen`
