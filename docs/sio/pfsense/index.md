12/2022

# Projet encadré: Création d'une zone démilitarisée avec pFsense

## Présentation

Dans le cadre de l'épreuve E5 du BTS SIO j'ai installé avec [mon coéquipier](https://62c3001898ccd.site123.me/) un pare-feu pFsense virtuel sur l'hyperviseur ESXI. Le but était d'ouvrir une DMZ.


Je détaillerais dans cette section la documentation du projet.

## Pré-requis

* OS opensource pFsense 2.6.0
* Hyperviseur ESXI 6.5 ou ultérieur
* Au moins 15GO stockage
* au moins 2GB RAM (dépend de l'utilisation)
* Au moins 3 interfaces réseau (WAN, LAN, DMZ)

## Objectifs



* Le serveur web est accessible depuis l’extérieur du réseau local
* Le réseau local non accessible depuis l’extérieur
* Le serveur web accessible depuis le réseau local
* Internet est accessible depuis le réseau local

### Schémas

* Schémas des flux de connexion:

![Diagramme de déploiement](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/diagramme_deploiement.png "Diagramme de déploiement, schéma des flux")

* Diagramme d'utilisation:


![Diagramme d'utilisation](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/diagramme_utilisation.png "Diagramme d'utilisation")

## Planification du projet

Voici comment était prévue la planification du projet:


![gantt_prev](https://github.com/1Tyron140/doc/raw/main/images/pfsense/gantt_prev.PNG)

Voici la comment elle s'est déroulée:

![gantt_reel](https://github.com/1Tyron140/doc/raw/main/images/pfsense/gantt_reel.PNG).

* L'élaboration des diagrammes et la liste des équipements a été plus rapide que prévu.

* Les règles ont pu être crées en même temps que la configuration et l'installation car les schémas aidaient et la prise en main de pfsense est simple et accompagnée de de documentation claire.


