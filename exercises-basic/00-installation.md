# Installation

Premier réflexe : la [documentation](https://laravel.com/docs/master) 

L'objectif de cet exercice est d'installer et configurer un environnement de travail avec Symfony


### PHP

Pour toute la suite des exercices, il est important d'avoir PHP installé sur votre machine (via Wamp, Mamp ou autres...)
et qu'il soit accessible en variable d'environnement.

Pour tester s'il est accessible ouvrez un terminal/console et tapez:

```bash
php -v
```

Si quelque chose comme ci-dessous apparait, c'est bon !

```bash
PHP 7.1.8 (cli) (built: Aug 17 2017 11:34:56) ( NTS )
```

dans le cas contraire, il faut procéder à quelques manipulations

> Sous Windows
> 
> Allez dans Panneau de configuration puis Système et sécurité puis Sécurité/Système. Ici se trouve un bouton "Paramètre de système avancé".
> Cliquez sur variables d’environnement.
> Il vous faut maintenant ajouter le chemin d’accès vers votre exécutable PHP (php.exe) à la variable d’environnement PATH.

> Sous MacOS / Linux
>
> Normalement, PHP est déjà présent sur l'OS. Si vous utilisez un serveur local de type Mamp ou autre,
> il est possible que vous ayez 2 versions de PHP sur votre machine. Pensez à bien tout maintenir à jour 
> pour éviter les conflits.


### Composer

Composer est un gestionnaire de dépendance pour PHP.

Vous pouvez le télécharger [ici](https://getcomposer.org/download/). Les commandes indiquées permettent de l'installer gloabalement sur votre machine.

Pour voir s'il est fonctionnel :
```bash
composer -v 
```

Dans le cas où l'installation globale de composer ne fonctionne pas, il est tout à fait possible 
de mettre le fichier `composer.phar` à la racine de votre projet et de l'utilser ainsi :
```bash
php composer.phar -v 
```


### Laravel

Pour la mise en place d'un nouveau projet Laravel, 2 approches sont possibles

D'une part, utiliser le "laravel installer". Il s'agit d'installer laravel globalement sur votre machine via composer.
Personnellement, je n'en vois pas un grand intérêt.

L'autre possibilité, utiliser simplement composer.

Placez-vous dans le dossier de votre projet :

 ```bash
composer create-project laravel/laravel blog
 ```


### Serveur local

Maintenant, il faut mettre en place notre serveur local pour le fonctionnement de Laravel.
Plusieurs possibilités se présentent à nous encore une fois:

- vous avez votre propre environnement de travail (Mamp, Wamp, Xamp, truc en amp, Linux...)

- Laravel fournis également un serveur local

 ```bash
php artisan serve
 ```

- La documentation Laravel fournis également 2 packages complets d'environnement serveur permettant d'aller
plus loin. Le but de ce cours n'est pas d'approfondir ces notions là qui s'approchent plus du réseau que du
développement.

Voici quand même les liens vers [Homestead](https://laravel.com/docs/master/homestead) et [Valet](https://laravel.com/docs/master/valet)



Une fois, tout en place, accédez à votre site et passez à l'execice suivant.