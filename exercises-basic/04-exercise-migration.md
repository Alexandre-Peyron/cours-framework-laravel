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

> Par convention, Laravel met les noms de table au pluriel.

```bash
php artisan make:migration create_article_table --create=articles
```

`create_article_table` sera le nom du fichier de migration.

L'option `--create` pré-rempli la migration avec la création d'une nouvelle table.

Un fichier a été créé : `database/migrations/*`

Vous pouvez à présent, modifier le fichier comme suit :

```php
Schema::create('articles', function (Blueprint $table) {
    $table->increments('id');
    $table->string('title');
    $table->text('content');
    $table->boolean('is_enabled');
    $table->timestamps();
});
```

Chaque ligne ajoute une propriété à notre table articles.

A noter que l'ID et les timestamps (created_at, updated_at) sont automatiquement gérés par Laravel.

Pour mettre à jour votre BDD, la commande est la suivante :

```bash
php artisan migrate
```

Vérifiez le contenu de votre base de données.

> En cas d'erreur à la génération. 
> Du type :  Key too long error
> Une solution est présente [ici](https://laravel-news.com/laravel-5-4-key-too-long-error)


A présent ajoutons [des données dans notre BDD](./05-exercise-seeding.md)
