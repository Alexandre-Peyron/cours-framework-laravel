# Amélioration du test

Maintenant, nous allons ajouter la notion de catégories.

Modifiez le test ainsi :

```php

/**
 * @test
 */
public function itCanDisplayAllTransactions()
{
    $transaction = factory('App\Transaction')->create();

    $this->get('/transactions')
        ->assertSee($transaction->description)
        ->assertSee($transaction->category->name);
}
```

La nouvelle est :

```
ErrorException: Trying to get property of non-object
```

### Model

Comme pour l'exercice précédent, il manque le model

```bash
php artisan make:model Category
```

Et modifions les model pour créer les relations 

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;

class Transaction extends Model
{
    public function category()
    {
        return $this->belongsTo(Category::class);
    }
}
```

### Migration

Nouvelle erreur, pas de table, créons la migration :

```bash
php artisan make:migration create_categories_table --create=categories
```

Ajoutez un `$table->string('name');` à la migration.

Modifions la migration des transactions avec : `$table->unsignedInteger('category_id');`

> Sur un projet déjà en ligne, nous aurions du créer une nouvelle migration pour ça.
>
> Ici comme nous sommes encore en phase de développement, on peut se permettre de modifier une migration déjà existante.

Modifions également les factory pour créer des données de tests.
Créez un nouveau fichier `database > factories > CategoryFactory.php`

```php
<?php

use Faker\Generator as Faker;

/*
|--------------------------------------------------------------------------
| Model Factories
|--------------------------------------------------------------------------
|
| This directory should contain each of the model factory definitions for
| your application. Factories provide a convenient way to generate new
| model instances for testing / seeding your application's database.
|
*/

$factory->define(App\Category::class, function (Faker $faker) {
    return [
        'name' => $faker->word,
    ];
});
```

Mettons à jour celui des transactions également.

```php
<?php

$factory->define(App\Transaction::class, function (Faker $faker) {
    return [
        'description' => $faker->sentence(4),
        'category_id' => function() {
            return factory(App\Category::class)->create()->id;
        }
    ];
});
```

### View

A présent, toute notre configuration de model est ok. Modifions la view pour afficher les catégories.

Votre test devrait être fonctionnel.


