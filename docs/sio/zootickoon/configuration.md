# Configuration de la base de donnée et de wordpress

## Création de la base de donnée Wordpress

* Sur la page de xampp, je sélectionne phpMyAdmin

* Je séléctionne nouvelle base de donnée

![new database](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/new_database.PNG)

* Je la nomme "wordpress" et séléctionne l'encodage "utf8_general_ci"

* Par sécurité, j'ai aussi crée un compte utilisateur avec les droits sur la base wordpress uniquement afin de ne pa utiliser le compte root

* Onglet users, créer un utilisateur "wordpress"

![user wordpress](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/pma_users.PNG)

* Dans cette l'onglet base de donnée de l'utilisateur, donner tous les droits sur la base wordpress

![droits de l'user wordpress](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/pma_wordpress_droits.PNG)

## Configuration de wordpress

* Se connecter 127.0.0.1/wordpress et cliquer sur "c'est parti"

* J'entre mes informations de connection à la base de donnée:
![setup_db](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/setup_db.PNG)

* "Envoyer"

* Et je désormais me connecter à l'interface d'admnisitration ou consulter le site vierge

![page admin](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/wp-admin.PNG)


