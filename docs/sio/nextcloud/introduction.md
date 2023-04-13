21/01/2023

# Installation d'un serveur de cloud interne Nextcloud

Ce projet a été réalisé en milieu professionnel. Le but est d'installer Nextcloud en interne afin d'avoir une solution de stockage de fichier servant aussi d'espace de travail pour le service.
<br><br>

## Introduction
 
Nextcloud est un logiciel de stockage en réseau. Cette solution est intéressante car on peut tout gérer en interne sur notre propre infrastructure contrairement à google drive, par exemple, où nos données sont gérée par quelqu'un d'autre. Dans ce document je vais vous montrer l'installation sur une machine linux **openSUSE 15.3**.

<br><br>
## Prérequis

On a besoin:

* D'une connexion internet
* Un OS pour le côté serveur (openSUSE)
* Une IP fixe sur le réseau
* Minimum 512 Mo de RAM

On installera:

* Une base de donnée (mariaDB)
* Un serveur web (apache)
* PHP

Plus de possiblités sur ce [lien](https://docs.nextcloud.com/server/latest/admin_manual/installation/system_requirements.html)

<br><br>

## Sources de documentation
* [Documentation Nextcloud](https://docs.nextcloud.com/server/latest/admin_manual/contents.html)
* [Site openSUSE](https://en.opensuse.org/SDB:Nextcloud)
