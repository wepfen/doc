# Sauvegarde du pFsense avec AutoConfigBackup

AutoConfigBackup est une fonctionnlité intégrée à pFsense qui permet de faire des sauvegardes en envoyant automatiquement la configuration vers les serveurs de Netgate (concepteur) de pFsense.

* Tout d'abord il faut établir un plan de sauvegardes
* Soit réaliser une sauvegarde à chaque modification
* Soit à une date précise



* J'ai choisi de l'effectuer à 6h00 tous les jours

![configuration autoconfigbackup](https://github.com/1Tyron140/doc/raw/main/images/pfsense/acb_settings.PNG)

* Je peux ensuite restaurer n'importe quelle sauvegarde en cliquant sur la flèche

![restauration backup autoconfigbackup](https://github.com/1Tyron140/doc/raw/main/images/pfsense/acb_restore.PNG)

* Mais aussi réaliser des sauvegardes manuelles

![backup manuelle](https://github.com/1Tyron140/doc/raw/main/images/pfsense/acb_manual_backup.PNG)