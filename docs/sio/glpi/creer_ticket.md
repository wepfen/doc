# Créer et suivre un ticket

## Qu'est-ce qu'un ticket

Un ticket permet de regrouper les informations du demandeur et le problème qu'il rencontre, ou la demande effectuée. Cela permet de effectuer un suivi de la demande, rendre-compte de la solution et garder une trace de chaque opération.

## Créer un ticket sur GLPI

### Les modalités d'ouverteture

Un ticket peut être ouvert,

* Par mail
* Par le technicien
* Par le service-helpdesk
* Par un utilisateur avec le rôle self-service

### Création du ticket

* Assistance > Créer un ticket

![creation d'un ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/creer_ticket_1.PNG)

* **Type** : Indiquer s'il s'agitd'un incident ou d'une demande
* **Statut** : C'est un nouveau ticket donc je le qualifie de nouveau
* **Source de la demande** : Indiquer par quel canal lle problème a été signalé initialement

![creation d'un ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/creer_ticket_2.PNG)

* **Urgence** : Urgence donnée par l'utilisateur
* **Impact** : Plus l'impact a des repercussions negatives sur le business plus l'impact est haut
* **Priorité** : Combinaison de l'urgence et de l'impact

![creation d'un ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/creer_ticket_3_demandeur.PNG)

* **Demandeur :** L'utilisateur qui rencontre un problème
* **Observateur :** La ou les personnes pouvant voir l'avancement d'un ticket, souvent le responsable de l'utilisateur
* **Attribué à** : Le technicien qui sera chargé de résoudre l'incident

![creation d'un ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/creer_ticket_4_elements.PNG)

* **Éléments** : Choisir le matériel concerné

![creation d'un ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/creer_ticket_5_description.PNG)

* **Titre** : Le titre du ticket
* **Description** : Décrire le soucis rencontré
* Cliquer sur le "+" en bas à droite pour créer le ticket

![creation d'un ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/creer_ticket_6_resultat.PNG)

* Voici le ticket affiché dans la liste des tickets

## Réaliser le suivi du ticket

Après avoir ouvert le ticket on peut réaliser le suivi, ajouter des informations et des solutions.

* Ouvrir la liste des tickets `Assistance > Tickets`

![Liste des tickets GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/menu_tickets.PNG)

* Sélectionner le ticket précédemment ouvert

* Cliquer sur réponse pour ajouter une réponse

![Repondre au ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/repondre_ticket.PNG)

![Reponse au ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/reponse_ticket.PNG)

* Sur la petite flèche à côté de "répondre", cliquer sur ajouter une solution

![Ajouter une solution au ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/solution_ticket.PNG)

* Une fois la solution ajoutée, il st possible de demander une validation ou de valider soit même après accord de l'utilisateur

![Approuver une solution au ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/approuver_solution_ticket.PNG)
