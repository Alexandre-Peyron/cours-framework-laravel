# Base de données et migrations

Première chose à faire, comme toujours, ouvrir la [documentation](https://laravel.com/docs/5.6/migrations) !

Le but de l'exercice est de comprendre le système de base de données avec Laravel. 

### Env

La configuration pour la connexion à votre base de données se passe dans le fichier .env à la racine du projet.

Modifier les lignes suivantes :

```text
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_blog
DB_USERNAME=root
DB_PASSWORD=root
```

Ces variables sont ensuite utilisées dans le fichier : `config/database.php`


### Migration

L'approche Laravel est intéressante de ce point de vue car elle met en place, dès le départ, un système de 
versionning pour la base de données.

> Ainsi chaque développeur peut apporter des modifications sur la BDD et tout le monde en est informé.
> Le Build de BDD se fait également plus facilement.

La première étape est de taper la commande suivante :

```bash
php artisan make:migration create_article_table --create=article
```

create_article_table sera le nom du fichier de migration.

L'option --create pré-rempli la migration avec la création d'une nouvelle table.

Un fichier a été créé : `database/migrations/*`

Vous pouvez à présent, modifier le fichier comme suit :

```php
Schema::create('article', function (Blueprint $table) {
    $table->increments('id');
    $table->string('title');
    $table->text('content');
    $table->boolean('is_enabled');
    $table->timestamps();
});
```

Chaque ligne ajoute une propriété à notre table article.

A noter que l'ID et les timestamps (created_at, updated_at) sont automatiquement gérés par Laravel.

Pour mettre à jour votre BDD, la commande est la suivante :

```bash
php artisan migrate
```

Vérifiez le contenu de votre base de données.


### Premières requêtes

Déplacez les actions de controller (/articles et /article/{index}) dans un [controller spécifique](https://laravel.com/docs/5.6/controllers).

Ajouter de fausses données en base de données pour vos articles.

Modifier vos actions de controller et vos vues pour afficher la liste des articles et un article spécifique depuis les valeurs de votre BDD.

