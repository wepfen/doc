# Inventaire du parc informatique grâce à FusionInventory sur GLPI - Windows Server

Ce projet est sous-jacent au projet GLPI.
FusionInventory sert à faire l'inventaire des différents postes de travail du parc informatique et renvoie par exemple:
- Le modèle de l'appareil
- Les logiciels installés
- Le nom de l'appareil
- ...

## Matériel utilisé

- Windows Server 2016 avec GLPI
- Une machine cliente windows 10 ( fonctionne aussi sous Linux)
- Plugin FusionInventory-server pour le serveur
- Agent FusionInventory pour les machines clientes

## Installation de FusionInventory

### Installation de FusionInventory-server

* Être connecté sur le serveur
* Se rendre sur le [site de fusioninventory](https://fusioninventory.org/)
* Cliquer sur `FusionInvetory for GLPI`

![site de fusioninventory](https://github.com/1Tyron140/doc/raw/main/images/glpi/site-fi.PNG)

* Télécharger le zip

![dépôt git de fusioninvetory](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi-git.PNG)

* Déziper et placer le dossier dans le sous dossier 'plugins' de GLPI du dossier wamp ou xampp

![Dossier plugins](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi-dossier-plugins.PNG)

* Se connecter à GLPI et ouvrir Configuration > Plugins

![menu glpi](https://github.com/1Tyron140/doc/raw/main/images/glpi/glpi_plugins.PNG)

* Puis cliquer sur l'icône de dossier

![Installer fusion inventory](https://github.com/1Tyron140/doc/raw/main/images/glpi/installer_fi.PNG)

Installation en cours

![Installation](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_installation.PNG)

* Dans `Configuration> Plugins`Activer fusion inventory en cliquant sur le bouton rouge.

![Activation](https://github.com/1Tyron140/doc/raw/main/images/glpi/activer_fi.PNG)

Voila ! FusionInventoryServer est installé

### Installation FusionInventory-agent (côté client)

* Sur le [site](https://fusioninventory.org/) de fusionInventory, choisir cette fois ci choisir "FusionInventory agent" 

* Télécharger la bonne architecture, je suis sur une machine windows 10 en 64 bits alors je prends la version x64 .exe:

![Dépôt git fusioinventory agent](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi-agent-git.PNG)

* Lancer l'éxécutable et configurer comme bon vous semble, voici mon installation:

![composants](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_agent_composant.PNG)

![URL de destination](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi-agent-destination.PNG)

![Option serveur HTTP local](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_agent_option-serveur.PNG)

![Options diverses](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_agent_divers.PNG)

J'ai choisi de lancer l'inventaire automatiquement mais voici comment le faire manuellement

* À la fin de l'installation, se connecter à [127.0.0.1:62354](http://127.0.0.1:62354) ou rechercher fusioninventory dans la barre de recherche windows

![resultat de recherche windows fusion inventory](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_agent_searchbar.PNG)

* Cliquer sur "Force Inventory"  

![force l'inventaire](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_agent_forceinventory.PNG)

Les données ont désormais été envoyées au serveur GLPI
Dans le cas contraire:

```
Vérifier que le serveur GLPI est bien accessible par la machine 
Vérifier que l'URL renseignée est correcte
Consulter les logs pour plus d'informations sur windows: `C:\Program Files\FusionInventory-Agent\logs`
```


* Ensuite, se connecter à GLPI
* `Administration > FusionInventory > Général > Gestion des Agents`

![Chemin vers la gestion des agents](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_gestion-agents.PNG)

On voit la liste des machines ayant utilisé un agent

![Liste des agents](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_liste-agent.PNG)

* Les logiciels renvoyés

![Liste des logiciels](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_logiciels.PNG)

* Ainsi que des informations précises sur les machines inventoriées

![Liste des ordis](https://github.com/1Tyron140/doc/raw/main/images/glpi/fi_liste_ordis.PNG)