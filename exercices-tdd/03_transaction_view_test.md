# Premier test

Nous allons créer une application de gestion de budget.

Un budget correspond à un ensemble de transaction sur une période (1 mois).
Et chacune de ces transactions peut être catégorisées.

# Test 1 - Peut-on afficher la liste de toutes les transactions ?

Créons notre premier test. Celui-ci va nous permettre de vérifier que la liste des transactions de notre application est fonctionnel

Pour créer un fichier de test, Laravel fournit des outils pour ça :

```bash
php artisan make:test ViewTransactionsTest
```

Une nouvelle class vient d'être créer dans `tests > Features`.

```php
<?php

namespace Tests\Feature;

use Tests\TestCase;
use Illuminate\Foundation\Testing\WithFaker;
use Illuminate\Foundation\Testing\RefreshDatabase;

class ViewTransactionsTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {
        $this->assertTrue(true);
    }
}
```

Il n'est pas nécessaire de conserver cette première méthode nous allons la réécrire.

> Pour que votre test soit pris en compte par PHPUnit vous avez 2 solutions
> - préfixer le nom de votre fonction par `test`
> 
> ou
>
> - ajouter l'annotation `@test` dans la documentation de votre fonction


### Première méthode

```php
<?php

/**
 * @test
 */
public function itCanDisplayAllTransactions()
{
    // crée une fake transation
    $transaction = factory('App\Transaction')->create();

    // essaie d'afficher la page /transactions
    $this->get('/transactions')
        ->assertSee($transaction->description); // Test si le text en paramètre est présent dans la page
}
```

Première chose, ma méthode est bien annoté avec @test.

Dans le fonctionnement, tout d'abord nous créons de fausses données avec la méthode factory.
Ensuite nous chargeons la page `/transactions` et en dernier nous effectuons un test.

Test qui est de savoir si oui/non la description de la transaction s'affiche dans la page.

### Effectuer le test

Notre code va partir de ce test.

Effectuons le.

```bash
./vendor/bin/phpunit --filter=itCanDisplayAllTransactions
```

L'option `--filter` permet de ne lancer qu'une seule méthode à la fois.

Avec un projet grandissant, on peut se retrouver avec plusieurs centaines de tests, il n'est pas nécessaire de tous les lancer à chaque fois.

Exécutez le test.

### Itération sur le code - Model

Une erreur doit s'afficher :

```
Error: Class 'App\Transaction' not found
```

C'est normal nous n'avons pas encore de model `Transaction`.

Pour corriger ce point, créons un nouveau modal

```bash
php artisan make:model Transaction
```

Un nouveau fichier vient d'être créé dans `app`.

Mais cela ne suffit pas. Il nous faut également des factories.

Dans le dossier `database > factories` créez un nouveau fichier `TransactionFactory`:

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

$factory->define(App\Transaction::class, function (Faker $faker) {
    return [
        'description' => $faker->sentence(4), // Crée une fausse description de 4 mots
    ];
});
```

Maintenant, relancez le test


### Itération sur le code - Database

Nouvelle erreur :

```
PDOException: SQLSTATE[HY000] [1045] Access denied for user 'homestead'@'localhost' (using password: YES)
```

La configuration de connexion à notre base de données est fausse.

Corrigez ce point.

Et relancez le test.


### Itération sur le code - Migration

Nouvelle erreur :

```
PDOException: SQLSTATE[42S02]: Base table or view not found: 1146 Table 'laravel_tdd.transactions' doesn't exist
```

Il n'existe pas de table Transaction dans notre base de données.

Normal, nous n'avons pas encore créé de migration associée.

```bash
php artisan make:migration create_transaction_table --create=transactions
```

Et modifiez la méthode de création ainsi :

```php
<?php
/**
 * Run the migrations.
 *
 * @return void
 */
public function up()
{
    Schema::create('transactions', function (Blueprint $table) {
        $table->increments('id');
        $table->string('description');
        $table->timestamps();
    });
}
```

Executez le test.

L'erreur existe toujours. Nous n'avons pas indiquer au test d'éxecuter les migrations.

Pour cela, modifiez la class de test pour ajouter le trait `RefreshDatabase`.

```php
class ViewTransactionsTest extends TestCase
{
    use RefreshDatabase;
```

Exécutez le test encore une fois.


### Itération sur le code - Error rendering

Nous avons une nouvelle erreur. Le problème ici, c'est qu'on affiche du HTML et c'est illisible dans la console.

Pour cela, nous allons modifier la class `TestCase dont nos class de tests héritent.

Ouvrez le fichier `tests/TestCase.php`

Modifiez la ainsi :

```php
<?php

namespace Tests;
use Exception;
use Illuminate\Foundation\Testing\TestCase as BaseTestCase;
use App\Exceptions\Handler;
use Illuminate\Contracts\Debug\ExceptionHandler;

abstract class TestCase extends BaseTestCase
{
    use CreatesApplication;
    
    protected function setUp ()
    {
        parent::setUp();
        $this->disableExceptionHandling();
    }
    
    protected function disableExceptionHandling ()
    {
        $this->oldExceptionHandler = app()->make(ExceptionHandler::class);
        app()->instance(ExceptionHandler::class, new PassThroughHandler);
    }
    
    protected function withExceptionHandling ()
    {
        app()->instance(ExceptionHandler::class, $this->oldExceptionHandler);
        return $this;
    }
}

class PassThroughHandler extends Handler
{
    public function __construct () {}
    public function report (Exception $e) {}
    public function render ($request, Exception $e)
    {
        throw $e;
    }
}

```

Pour explication, ici nous désactivons le rendu d'erreur par défaut pour afficher seulement l'erreur PHP.

Cela rend la lecture beaucoup plus lisible


### Itération sur le code - Routing et controller

L'erreur est donc la suivante :

```
Symfony\Component\HttpKernel\Exception\NotFoundHttpException: 
```

Il manque la route.

Dans le fichier web, ajoutez :

```php
Route::get('/transactions', 'TransactionsController@index');
```

Nouvelle erreur :

```
ReflectionException: Class App\Http\Controllers\TransactionsController does not exist
```

Le controller n'existe pas.

Créez le :

```bash
php artisan make:controller TransactionsController
```

La méthode index n'existe pas.

```php
public function index()
{

}
```

### Itération sur le code - View

Il faut à présent créer l'action de controller et la view correspondante.

Pour se faciliter la vie, nous allons utiliser les templates de bases de Laravel.

Pour cela, activons l'authentification

```bash
php artisan make:auth
```

A présent dans `ressources/views`, créons un nouveau dossier `transactions`.
Ainsi qu'un fichier `index.blade.php`

```blade
@extends('layouts/app')

@section('content')
    <div class="container">
        <div class="table-responsive">
            <table class="table">
                plop
                <thead>
                    <tr>
                        <td>Date</td>
                        <td>Description</td>
                        <td>Montant</td>
                    </tr>
                </thead>
                <tbody>
                    @foreach($transactions as $transaction)
                        <tr>
                            <td>{{ $transaction->created_at->format('d-m-Y') }}</td>
                            <td>{{ $transaction->description }}</td>
                        </tr>
                    @endforeach
                </tbody>
            </table>
        </div>
    </div>
@endsection
```

et complétez l'action de controller 

```php
public function index()
{
    $transactions = Transaction::latest()->get();

    return view('transactions.index', compact('transactions'));
}
```

Le test doit être bon maintenant.
