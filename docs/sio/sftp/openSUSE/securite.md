# Capture avec wireshark 

On va tester avec wireshark voir si la communication est chiffrée ou non

## Installation

`zypper install wireshark`

* Lancer le programme en étant en root sinon les interfaces intéressantes seront indisponibles

* Sans root

![Wireshark sans privileges](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/wireshark_no_root.png "wireshark sans privilèges")

* Avec root 

![Wireshark avec privileges](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/wireshark_root.png "wireshark avec privilèges")


### Autoriser un utilisateur non-root à avoir toutes les interfaces

en root,

* Ajouter l'utilisateur souhaité au groupe wireshark

`usermod -aG wireshark user`

* S'assurer que le groupe wireshark puisse exécuter le binaire dumpcap, sinon faire:

`chmod g+x /usr/bin/dumpcap`

Si les changements ne s'appliquent pas, se déconnecter et se reconnecter

## Capture

la capture va s'effectuer avec l'interface "any"

* Lancer la capture

* Se connecter au SFTP 

* Filtrer la capture par ssh en tapant "ssh" puis entrer dans la barre de filtre

On peut voir que je me suis connecté au sftp avec Filezilla

![Wireshark avec privileges](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/wireshark_filezilla.png "connecté avec filezilla")

Et le contenu de ce paquet et de tous les autres est chiffré

![paquet chiffré](https://raw.githubusercontent.com/1Tyron140/doc/main/images/sftp/contenu_chiffré.png "Le contenu est bien chiffré")

