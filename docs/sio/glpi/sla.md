# Mettre en place et utiliser les SLA

## Définition des SLAs

Les SLA (service level agreement) ou accord de niveau de service permettent de définir un délai maximum de résolution d'un ticket. Ainsi il est possible d'évaluer l'efficacité d'un technicien.

Les SLA sont composés de deux indicateur:

### TTR et TTO

* **TTO** (Time to own), délai garanti d'assignation d'un ticket
* **TTR** (time to resolve), délai garanti de résolution d'un ticket

Ces deux valeurs seront variables selonn lapriorité d'u ticket

## Mise en place des SLAs

Sur un ticket on retrouve le champ **niveau de service** avec les champs TTR et TTO.

![niveau de service ticket GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/niveau_service_ticket.PNG)

On peut les remplir selon la date du jour ou alors selon une durée précise.
Pour cela il faudra créer un niveau de service puis créer des valeurs de TTR et TTO


* Configuration > Niveaux de services
* Cliquer sur le "+"
* Choisir un nom et ajouter

![liste niveau de service GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/liste_niveaux_services.PNG)

* Puis cliquer sur le niveau de services précédemment crée
* Cliquer sur "SLAs"
* Choisir un titre comme "TTR[durée de résolution]"

![creation de TTR GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/creation_ttr.PNG)

Voila un exemple d'une liste des SLAs

![liste des slas GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/liste_sla.PNG)

Désormais je peux maintenant séléctionner les SLA sur mon ticket

![ticket avec sla GLPI](https://raw.githubusercontent.com/1Tyron140/doc/main/images/glpi/ticket_avec_sla.PNG)

Les TTR internes et TTO internes peuvent être crées comme les SLA mais en selectionnant "OLA" plutôt que "SLA".