# Controller

Qu'est-ce qu'on ouvre en premier ? La [documention](https://laravel.com/docs/master/controllers) ! (again and again and again)

Jusqu'à présent, on a travaillé dans le fichier `routes/web.php`. Ce n'est pas très propre.

Le but de ce fichier est de définir les routes, pas d'avoir du code fonctionnel.

On va donc décentraliser le code pour avoir des class de controller spécifique.

Entrez la commande suivante :

```bash
php artisan make:controller ArticleController -r
```

L'option -r (ou --resource) permet de générer au passage, les actions de controller de base. 
Dans les bonnes pratiques de Laravel, les actions sont réparties ainsi :


| Method    | URL                 | Action  | Route name       | 
|-----------|---------------------|---------|------------------|
| GET       | /articles           | index   | articles.index   |
| GET       | /articles/create    | create  | articles.create  |
| POST      | /articles           | store   | articles.store   |
| GET       | /articles/{id}      | show    | articles.show    |
| GET       | /articles/{id}/edit | edit    | articles.edit    |
| PUT/PATCH | /articles/{id}      | update  | articles.update  |
| DELETE    | /articles/{id}      | destroy | articles.destroy |

Dans votre fichier web.php, il n'est pas nécessaire ensuite d'importer chaque route de manière indépendante.
Mais la ligne suivante devrait faire le travail :

```php
<?php

Route::resource('articles', 'ArticleController');

```

Nous allons maintenant travailler dans ce controller pour compléter chacune des route manquante.

Mise en place de [notre première migration](./04-exercise-migration.md)

