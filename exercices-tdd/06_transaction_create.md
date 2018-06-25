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


