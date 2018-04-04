# Seeding

Première chose à faire, comme toujours, ouvrir la [documentation](https://laravel.com/docs/master/seeding) !

Laravel fourni un outil pour générer à la volée vos données de tests. Cela s'appelle le seeding (des Fixtures chez Symfony)

### Premier seeding

Nous allons maintenant générer une nouvelle class pour avoir des données de test pour nos articles.

```bash
php artisan make:seeder ArticlesTableSeeder
```

Le fichier ArticlesTableSeeder.php `vient d'être créé dans` database/seeds`.

Ajoutez ceci à la méthode run :

```php
<?php
DB::table('articles')->insert([
    'title'      => str_random(10),
    'content'    => str_random(100),
    'is_enabled' => (bool)random_int(0, 1) // PHP 7 - Aléatoirement true ou false
    //'is_enabled' => rand(0,1) == 1; // PHP 5
]);
```
Trouvez un moyen de générer une date aléatoire (pour le created_at) entre aujourd'hui et les 10 derniers jours.

Créez maintenant une boucle for pour générer une dixaine d'articles aléatoire.

Avant de pouvoir mettre à jour notre BDD, il faut modifier le fichier `database/seeds/DatabaseSeeder.php`.
Celui-ci centralise l'appel de tous les autres seed. A vous d'ajouter les `call` nécessaires dans sa méthode run.

La commande suivante va mettre à jour votre BDD :

```bash
php artisan db:seed

php artisan db:seed --class=ArticlesTableSeeder
```

La commande suivante sert mettre à jour les tables votre BDD ainsi que les seeds associés :

```bash
php artisan migrate:refresh --seed
```

> En cas d'erreur, il est possible que vous ayez besoin de mettre à jour les autoloader :
> `composer dump-autoload

