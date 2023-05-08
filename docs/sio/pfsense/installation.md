# Installation de pFsense sur ESXI

Dans cette partie on va voir comment installer une machine virtuelle pfsense sur un hyperviseur ESXI

## ESXI

### Télécharger l'ISO
* Tout d'abord il faut installer l'ISO sur [le site officiel de pfsense](https://www.pfsense.org/download/)

![Site de telechargement pfsense](https://github.com/1Tyron140/doc/raw/main/images/pfsense/site_pfsense.PNG)

* Extraire le fichier le compressé 

* Sur le esxi, entrer dans le Datastore

![Datastore ESXI](https://github.com/1Tyron140/doc/raw/main/images/pfsense/datastore.PNG)

* Créer un répertoire "ISO" où l'on va venir ranger les ISO (facultatif), puis sur télécharger

![datastore créer répertoire](https://github.com/1Tyron140/doc/raw/main/images/pfsense/contenu_datastore.PNG)

* Entrer dans le dossier ISO

* Sélectionner l'ISO

![selectionner fichier iso](https://github.com/1Tyron140/doc/raw/main/images/pfsense/pfsense_iso.PNG)

* Le téléchargement s'effectue

![telechargement en cours](https://github.com/1Tyron140/doc/raw/main/images/pfsense/iso_vers_esxi.PNG)

Pendant que le téléchargement mijote, on va préparer la VM


### Paramétrage de la VM pFsense

* Sur la barre latérale, cliquer sur "Machines Virtuelles" puis créer
    * Nom: ce que vous voulez
    * Stockage: datastore, => 15GB
    * CPU: 2
    * Système d'exploitation: autre > FreeBSD
    * Mémoire: => 2GB
    * Adaptateur réseau: VM Network
    * Lecteur de CD/DVD: mettre le chemin vers notre ISO quand il sera installé
    
![création VM](https://github.com/1Tyron140/doc/raw/main/images/pfsense/config_machine.PNG)

Au démarrage, la VM boot sur le réseau. Il faut modifier ce comportement dans le BIOS de la VM.
Le délai pour appuyer sur la touche est assez cours alors on va l'augmenter.

* VM > Option VM > Option de démarrage:
    * Délai de démarrage: 30000 ms
    * Forcer la configuration BIOS
	
* Ou alors "forcer l'entrée dans l'écran de configuration du bios au prochain démarrage"
    
![Option de démarrage](https://github.com/1Tyron140/doc/raw/main/images/pfsense/option_demarrage_042016.PNG)

### Installation


* Au démarrage le menu BIOS sera donc lancé
* Dans la section `Boot`, faire passer `CD-ROM` en premier à l'aide de la touche "+"
* Sauvegarder et quitter avec "F10"

![Menu BIOS](https://github.com/1Tyron140/doc/raw/main/images/pfsense/ordre_boot_042017.PNG)

* Lors de l'installation laisser les valeurs par défaut et poursuivre

![Page welcome installation pfsense](https://github.com/1Tyron140/doc/raw/main/images/pfsense/pfsense_welcome.PNG)

* Choisir le clavier français avec espace puis entrée (bien qu'il restera en QWERTY ensuite)

![choix clavier pfsense](https://github.com/1Tyron140/doc/raw/main/images/pfsense/pfsense_keymap_selection.PNG)

* Pour le disque j'ai choisi ZFS mais UFS (BIOS ou UEFI) fonctionne très bien aussi

![pfsense partitionnement](https://github.com/1Tyron140/doc/raw/main/images/pfsense/zfs.PNG)

![ZFS configuration pfsense](https://github.com/1Tyron140/doc/raw/main/images/pfsense/zfs_conf.PNG)

* Choisir "non" pour la configuration manuelle sur shell

![configuration manuelle pfsense](https://github.com/1Tyron140/doc/raw/main/images/pfsense/manual_configuration_pfsense.PNG)

* faire entrée sur `Reboot` pour redémarrer et finaliser l'installation

![installation complétée pfsense](https://github.com/1Tyron140/doc/raw/main/images/pfsense/pfsense_complete.PNG)

Ensuite il va falloir configurer les interfaces réseau dans la [partie suivante](https://tyron-docs.readthedocs.io/fr/latest/sio/pfsense/configuration.html) 


## Infrastructure

### Le plan d'action

Le plan d'action décrit comment je fais fonctionner le routage pFsense dans un premier temps alors il est important de le comprendre.

* L'idée est de configurer une machine virtuelle pFsense qui sera connectée à chaque interface réseau de l'ESXi dont une reservée pour le WAN ou seul le pFsense sera présent.
* Le port WAN sera connecté au routeur vers l'internet par RJ45
* Les autres ports (LAN, DMZ, SERVEURS) seront connectés par RJ45 vers leurs switches respectifs
* Le routage vers ces switchs s'effectuera par pfsense
* L'interface du routeur cisco (ou votre box) sera connecté avec pFsense par une IP statique choisie et vice-versa pour pFsense.
* Du côté LAN, DMZ, SERVEURS, pFsense sera la passerelle pour ces sous-réseaux
* Donc il faudra avant de brancher le pFsense au routeur, me brancher au switch ou st présent l'hyperviseur, m'y connecter et configurer l'interface vers internet sur pFsense.
* Puis brancher 
* Le pFsense est maintenant branché au routeur vers l'internet, je ne peux que me brancher au switches LAN, DMZ ou serveurs.
* La l'ESXi n'a pas accès à internet car le pfsense n'effectue pas encore le routage donc l'hyperviseur ESXi aura une adresse link-local(169.254.0.0/16)
* L'ESXi est branché à un écran donc je peux savoir l'ip après un petit temps
* Je me configurer une IP statique link-local sur mon PC puis j'accède à l'ESXi et je configure le pFsense d'ici
* Désormais je peux séléctionner une IP pour le pFsense sur chaque sous-réseaux, activer le DHCP, et mettre en place les règles pour accéder à internet.


### Branchements

* Branchements sur le routeur

![cisco 2900](https://github.com/1Tyron140/doc/raw/main/images/pfsense/cisco_2900.jpg)

* Brachement sur l'hyperviseur ESXi

![esxi branchement](https://github.com/1Tyron140/doc/raw/main/images/pfsense/arriere_esxi.jpg)

>wan représente le routeur précédent

Grâce à ces branchements le pare-feu même étant virtuel, en place devant le réseau à protéger
Maintenant il faudra le configurer

* ESXi branché au switch serveurs locaux qui redistribuera ainsi le réseau grâce au pFsense


![switch](https://github.com/1Tyron140/doc/raw/main/images/pfsense/switch_serv.jpg)
