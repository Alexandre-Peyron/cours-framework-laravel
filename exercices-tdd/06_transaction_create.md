# Tester la création d'une transaction

L'objectif est ici de tester la création, via formulaire, d'une transaction.

### Test

Créons un nouveau fichier de test :

```bash
php artisan make:test CreateTransactionsTest
```

Et ajoutez le test suivant :

```php
<?php

namespace Tests\Feature;

use Tests\TestCase;
use Illuminate\Foundation\Testing\WithFaker;
use Illuminate\Foundation\Testing\RefreshDatabase;

class CreateTransactionsTest extends TestCase
{
    /**
     * @test
     */
    public function itCanCreateTransactions()
    {
        $transaction = factory('App\Transaction')->make();

        $this->post('/transactions', $transaction->toArray())
            ->assertRedirect('/transactions');

        $this->get('/transactions')
            ->assertSee($transaction->description);
    }
}
```

On reprend le même principe. On exécute le test, et on itère pour corriger les problèmes.

### Routing

Première erreur, la route n'existe pas.

```php
Route::post('/transactions', 'TransactionsController@store');
```

Deuxièmre erreur, la méthode n'existe pas.

On l'ajoute dans le controller 

```php
public function store() {

}
```

Nouvelle erreur :
```
Response status code [200] is not a redirect status code.
Failed asserting that false is true.
```

Aucune redirection n'a été effectuée, alors que le test attend précisément cela.

Modifions le controller pour ajouter en BDD et rediriger.

```php
public function store()
{
    Transaction::create(request()->all());

    return redirect('/transactions');
}
```

Modifiez à présent le model pour rendre les champs "description" et "category_id" ajoutables.


### Validation des champs

Notre test est fonctionnel mais il est encore faillible.

Notemment si on passe certains champs à `null`.

Ajoutons un test à notre class

```php
/**
 * @test
 */
public function itCannotCreateTransactionsWithoutADescription()
{
    $transaction = factory('App\Transaction')->make(['description' => null]);

    $this->post('/transactions', $transaction->toArray())
        ->assertSessionHasErrors('description');
}
```

Modifions notre controller store pour vérifier les données :

```php
$this->validate(request(), [
   'description' => 'required',
]);
```

L'erreur est la suivante : Illuminate\Validation\ValidationException: The given data was invalid.
                           
Dans un sens, c'est ce que nous voulons.

Modifions le test pour accepter ce genre d'erreur 

```php
$this->withExceptionHandling()->post('/transactions', $transaction->toArray())
     ->assertSessionHasErrors('description');
```

Effectuez le même travail pour la catégorie en créant une nouvelle fonction de test.

