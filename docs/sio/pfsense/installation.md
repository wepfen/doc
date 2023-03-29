# Installation

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
    
![Option de démarrage](https://github.com/1Tyron140/doc/raw/main/images/pfsense/option_demarrage_042016.PNG)


## Infrastructure

>Ce sont les branchments APRES avoir préconfiguré le pare-feu car une fois branché de la sorte on ne pourra plus l'administrer par son interface par le wan car il n'y a pas de port où brancher un pc portable.

* Chacune des interfaces réseau de l'hyperviseur est connecté au pFsense, la première servira à se brancher au routeur et les autres aux différents switch de sortes à transmettre le réseau.

* Le routeur sera branché à l'interface du ESXi avec PFSENSE et ce dernier fera le routage vers les switches et différents sous réseaux.

* Branchements sur le routeur

![cisco 2900](https://github.com/1Tyron140/doc/raw/main/images/pfsense/cisco_2900.jpg)

* Brachement sur l'hyperviseur ESXi

![esxi branchement](https://github.com/1Tyron140/doc/raw/main/images/pfsense/arriere_esxi.jpg)

>wan représente le routeur précédent

Grâce à ces branchements le pare-feu même étant virtuel, en place devant le réseau à protéger
Maintenant il faudra le configurer

* ESXi branché au switch serveurs locaux qui redistribuera ainsi le réseau grâce au pFsense


![switch](https://github.com/1Tyron140/doc/raw/main/images/pfsense/switch_serv.jpg)
