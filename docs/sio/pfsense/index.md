# PPE pFsense

## Présentation

Dans le cadre de l'épreuve E5 du BTS SIO j'ai installé un pare-feu pFsense virtuel sur l'hyperviseur ESXI. Le but était d'ouvrir une afin une DMZ.


Je détaillerais dans cette section la documentation du projet.

## Pré-requis

* OS opensource pFsense 2.6.0
* Hyperviseur ESXI 6.5 ou ultérieur
* Au moins 15GO stockage
* au moins 2GB RAM (dépend de l'utilisation)
* Au moins 3 interfaces réseau (WAN, LAN, DMZ)

## Objectifs

Voici le résumé du cahier des charges:

* Le serveur web est accessible depuis l’extérieur du réseau local
* Le réseau local non accessible depuis l’extérieur
* Le serveur web accessible depuis le réseau local
* Internet est accessible depuis le réseau local

* Schémas des flux de connexion  (diagramme de déploiement)

![Diagramme de déploiement](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/diagramme_deploiement.png "Diagramme de déploiement, schéma des flux")

* Diagramme d'utilisation

![Diagramme d'utilisation](https://raw.githubusercontent.com/1Tyron140/doc/main/images/pfsense/diagramme_utilisation.png "Diagramme d'utilisation")

(insérer gantt réel)
