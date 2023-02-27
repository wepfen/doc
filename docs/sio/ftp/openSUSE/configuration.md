# Configuration de vsftpd 

## Paramètres généraux

### Message de bienvenue

S'affiche après la connexion au FTP. 

Le choix est libre.

### Chroot

Permet de cloisonner chaque utilisateur dans un répetoire donné. Ainsi, le répertoire défini sera vu par l'utilisateur comme le répertoire racine et l'utilisateur ne pourra pas naviguer dans le système.

* Cocher "chroot pour tout le monde"

* Entrer le chemin du répertoire racine voulu dans "Répertoire FTP pour les utilisateurs authentifiés"

Voir plus dans sécurité > chroot de cette documentation.

### Journalisation détaillée

* Laisser cette option cochée

### Umask

Permet de définir les permissions par défaut d'un répertoire ou d'un fichier au format octal (exemple: 755).

* J'entre 640 pour les utilisateurs authentifiés.
* Je laisse vide pour les utilisateurs anonyme car je vais désactiver les users anonymes.

## Authentification

### Activer/désactiver les utilisateurs locaux et anonymes

* Uniquement les utilisateurs auhentifiés
* Pour rappel il s'agit des comptes utilisateurs présnts sur le serveur FTP ou synchronisés avec un LDAP (pas mon cas)
