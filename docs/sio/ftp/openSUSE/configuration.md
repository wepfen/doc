# Configuration de vsftpd 

## Paramètres généraux

### Message de bienvenue

S'affiche après la connexion au FTP. 

Le choix est libre.

### Chroot

Permet de cloisonner chaque utilisateur à son propre répetoire.

* Je coche

### Journalisation détaillée

* Laisser cette option cochée

### Umask

Permet de définir les permissions par défaut d'un répertoire ou d'un fichier.

À écrire au format octal (exemple: 755) 

* J'entre 640 pour les utilisateurs authentifiés
*  Je laisse vide pour les utilisateurs anonyme car je vais désactiver les users anonymes
