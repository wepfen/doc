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


### Paraétrage de la VM pFsense

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
