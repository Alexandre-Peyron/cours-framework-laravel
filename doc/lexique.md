# Lexique

## :blue_book: La documentation

### Définition
Pour chaque outil utilisé dans un projet web (IDE, Fremawork, librairie externe, gestionnaire de tâches...) une documentation existe.
C'est assez magique car cela explique comment fonctionne ce que vous voulez utiliser.

### Avantage
- répond à vos questions

### inconvénient
- aucun

## :blue_book: Framework

### Définition
En programmation informatique, un framework désigne un ensemble cohérent de composants logiciels structurels, qui sert à créer les fondations ainsi que les grandes lignes de tout ou d’une partie d'un logiciel (architecture). 
Un framewok définit un cadre de travail qu'il impose de par sa construction même, guidant l'architecture logicielle voire conduisant le développeur à respecter certains patrons de conception.
 
Un framework n'est pas un CMS. Mais peut constituer la base du code d'un CMS.

### Pourquoi utiliser un framework ?
L'utilisation d'un framework n'est pas indispensable, mais grandement conseillée.

L'objectif étant de ne pas ré-inventer la roue. Se concentrer sur la tâche et le fonctionnement métier et non sur la technologie derrière.

Il donne un cadre et une structure au code compréhensible par toute personne formée dessus.

Sur une vision long terme, il garantit la maintenance et l'évolution du votre projet. Grâce à la communauté qui fait vivre l'outil et (souvent) aux entreprises derrière qui en assurent sa pérennité.

### Quand utiliser un framework ?

Avec la multitude d'outils CMS, CRM, solution e-commerce l'utilisation d'un framework n'est pas toujours nécessaire.
Si un des outils précédents répond parfaitement à votre besoin, il faut l'utiliser.

L'usage d'un framework intervient dans le cadre d'un développement spécifique pour répondre à un besoin spécifique.

### Exemples

- [Symfony](https://symfony.com/)
- [Laravel](https://laravel.com/)

## :blue_book: Design Pattern

### Définition

En informatique, et plus particulièrement en développement logiciel, un patron de conception (souvent appelé design pattern) est un arrangement caractéristique de modules, reconnu comme bonne pratique en réponse à un problème de conception d'un logiciel. Il décrit une solution standard, utilisable dans la conception de différents logiciels.

[Source Wikipédia](https://fr.wikipedia.org/wiki/Patron_de_conception)

## :blue_book: MVC - Modèle-Vue-Controller

### Définition

Modèle-vue-contrôleur ou MVC est un motif d'architecture logicielle destiné aux interfaces graphiques lancé en 1978 et très populaire pour les applications web. Le motif est composé de trois types de modules ayant trois responsabilités différentes : les modèles, les vues et les contrôleurs.
- Un modèle (Model) contient les données à afficher.
- Une vue (View) contient la présentation de l'interface graphique.
- Un contrôleur (Controller) contient la logique concernant les actions effectuées par l'utilisateur.

Ce motif est utilisé par de nombreux frameworks pour applications web tels que Ruby on Rails, Symfony, Apache Tapestry, Laravel, AngularJs...

[Source Wikipédia](https://fr.wikipedia.org/wiki/Mod%C3%A8le-vue-contr%C3%B4leur)

> Liste des Design Patterns
>
> [En lien](https://github.com/domnikl/DesignPatternsPHP), la très belle liste des design pattern en PHP.

## :blue_book: Routing/Routage/Routeur

### Définition
Qu'il soit physique ou programmatique, un routeur à le même objectif : sélectionner un chemin dans un réseau.

Dans le cadre de la programmation, il va lire une URL pour déterminer l'action à effectuer.

## :blue_book: Controller

### Définition

Une fois le travail effectuer par le routeur, celui-ci va déterminer un action de controller à exécuter.

Une action de controller est une fonction PHP créez par vous qui va lire les informations reçues de la requête HTTP, effectuer un traitement et renvoyer une réponse.

## :blue_book: ORM

### Définition

Un mapping objet-relationnel (en anglais object-relational mapping ou ORM) est un type de programme informatique qui se place entre un programme applicatif et une base de données relationnelle pour simuler une base de données orientée objet. 
Ce programme définit des correspondances entre les schémas de la base de données et les classes du programme applicatif (Ici class en PHP). 
On pourrait le désigner par là, « comme une couche d'abstraction entre le monde objet et monde relationnel ». 

[Source Wikipédia](https://fr.wikipedia.org/wiki/Mapping_objet-relationnel)

### Avantage/Inconvénients

Utiliser un ORM facilite grandement l'usage d'une base de données pour des fonctionnements simples. Beaucoup choses automatisées.

A l'inverse, pour des besoins spécifiques, il peut devenir difficile d'utiliser un ORM.
 

### Exemples

- [Eloquent](https://laravel.com/docs/5.7/eloquent) : l'ORM de Laravel
- [Doctrine](https://www.doctrine-project.org/) : l'ORM de Symfony
- [Active Record](https://guides.rubyonrails.org/active_record_basics.html) : l'ORM de Ruby On Rails


## :blue_book: Moteur de template

### Définition

Un moteur de template permet de dissocier l'interface (HTML) de la partie programmation (PHP, JS...).

### Pourquoi utiliser un moteur de template ?

- Dans un modèle MVC, il permet de clairement dissocier la View (le design) du code métier
- Structure votre code 
- Gestion du cache et performances améliorées
- Rend le code plus lisible (l'inclusion de balise <?php ?> peut devenir très lourde et encombrante)

### Exemples

- [Blade](https://laravel.com/docs/5.8/blade) : Laravel
- [Twig](https://twig.symfony.com/) : Symfony
- [Smarty](https://www.smarty.net/)


## :blue_book: Gestionnaire de dépendances 

### Définition

Dans un projet de développement, on est très souvent amené à utiliser des librairies externes, que ça soit en CSS, JS ou PHP. 
Pour faciliter l'utilisation et la mise en place de ces dépendances, on utilise un gestionnaire de dépendance.
Cet outil à pour but de centraliser la liste des dépendances (et leurs versions) un fichier pour ensuite pouvoir les télécharger/importer en une ligne de commande.

### Avantages
- centraliser la liste des dépendances et leurs versions (si plusieurs personnes travaillent sur le projet, elles auront toutes les mêmes dépendances)
- facilite le téléchargement de ces ressources

### inconvénient
- si une dépendance est supprimée par son auteur, votre projet risque de ne plus fonctionner
- les contraintes de versions et de dépendances, de dépendances, de dépendances peuvent parfois être problématique

### Exemples

- [Composer](https://getcomposer.org/) : en PHP
- [NPM](https://www.npmjs.com/) : en JavaScript
- [Yarn](https://yarnpkg.com/) : en JavaScript 
- [Bundler](https://bundler.io/) : en Ruby


## :squirrel: Bonus

[La RoadMap pour devenir un développeur Web](https://github.com/kamranahmedse/developer-roadmap)
