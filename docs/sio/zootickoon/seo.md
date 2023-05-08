# Amélioration du référencement (SEO)

## Introduction au SEO

Le SEO pour "search engine optimization", permet d'optimiser une page web afin qu'elle soit mieux référencée par le navigateur web. 

Cela peut être effectué en structurant correctement une page, en ajoutant des imaes , des titres, des descriptions ou encore lorsque des siites externes ont des liens redirigant vers cette même page.

Sur wordpress certaines pratiques sont mise en oeuvre par défaut et des extensions comme **Yoast SEO** permettent d'aller plus loin

## Mise en oeuvre

Les sections suivantes décrivent ce que j'ai réalisé et permttent toutes d'améliorer le référencment SEO.

### Yoast SEO

Il s'agit d'une extension permettant d'assister le webmestre pour améliorer le référencement.

![](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/yoast.PNG)

### Texte alternatif

Le texte alternatif permet de décrire un objet de manière précise.
Voici comment j'ai rajouté un texte alternatif à une image sur wordpress:

* Sur la page en question en mode édition
* Cliquer sur l'image, un menu déroulant s'affiche
* Remplir la case "texte alternatif" avec texte clair et concis

![](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/exemple_texte_alt.PNG)


### Permettre l'indexation

Les crawlers sont des programmes qui parcourent les sites web et indexent les sites dans les moteurs de recherche si le "robots.txt" de chaque site les autoriser à le faire.

Sur l'interface d'administration Wordpress après avoir installé YOAST:

* Yoast SEO > Outils > Editeur de fichier > robots.txt
* Le créer s'il le faut 
* Enregistrer

![](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/robots.PNG)


Il est aussi important d'autoriser l'indexation du site das les paramètres:

![](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/activer_visibilite.PNG)

### Meta-description

La méta-description est la courte description de page visible sur le résultat d'une recherche sur un moteur de recherche.

Exemple:

![](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/meta-description-exemple.png)

Voici comment faire avec Yoast:

* Aller sur la page en mode édition
* Tout en bas
* Renseigner le champ "meta description:

![](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/metadescription_animaux.PNG)

### Titre H1

Le titre H1 est le titre qui être affiché sur le résultat d'une page web
Il convient de mettre un seul titre en h1 et en choisir un clair et concis

![](https://raw.githubusercontent.com/1Tyron140/doc/main/images/zootickoon/titre-h1-google.png)

* Sur wordpress il s'agit du premier titre saisi sur la page

### Autres méthodes

#### Les backlinks

Plus à lien ramenant vers votre site web est trouvé sur d'autre sites, mieux votre sites sera référencé. Et encore mieux si le lien est trouvé sur un site déjà très bien référencé.

Ce principe est expliqué en détail [ici](https://semji.com/fr/guide/backlink-en-seo/)

> Comme je viens de le faire à l'instant, j'ai crée un backlink vers le site "semji.com)

Cependant vous ne pouvez pas modifie le site d'une autre personne et ajouter votre lien, cela se fait habituellement dans les espaces commentaires par exemple.

L'abus de cette pratique est appelée [SEO poisonning](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiLo9TcouX-AhUtUKQEHRPgABcQFnoECAwQAQ&url=https%3A%2F%2Fwww.sekoia.io%2Ffr%2Fglossaire%2Fseo-poisoning%2F&usg=AOvVaw1O60ALwuIcCdF0ghsqgICu)

#### Avoir un site responsive

C'est-à-dire un site qui s'adapte selon l'écran utilisé. 
Avec un CMS comme Wordpress ou Wix, le site est automatiquement responsive.
Autrement, à moins d'utiliser un Framework comme Bootstrap, il faut mettre les mains dans le cambouis. 
Openclassroom montre comment le faire dans ce [cours](https://openclassrooms.com/fr/courses/1603881-creez-votre-site-web-avec-html5-et-css3/8061510-utilisez-le-responsive-design-avec-les-media-queries)


#### Et plus encore

Voici une [liste](https://blog.hubspot.fr/marketing/conseils-referencement-articles) plus complète.

## Conclusion

Le SEO est un ensemble de pratique qui doivent être respectée pour bien optimiser le référencement.
Cependant même avec un SEO bien réalisé, les résultats ne sont pas instantanés, il faut attendre que les "crawlers" vu plus haut fassent leur boulot.
En revanche avec un SEO peu travaillé, le site pourra quand même être référencé mais pas affiché dans les premiers résultats.



 