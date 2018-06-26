# Mise à jour Transaction

Nos tests d'ajouts et le formulaire fonctionne. La suite logique est donc l'update.


### Test Update

Ci-dessous le test pour l'update :

```php
<?php

namespace Tests\Feature;

use Tests\TestCase;
use Illuminate\Foundation\Testing\DatabaseMigrations;

class UpdateTransactionsTest extends TestCase
{
    use DatabaseMigrations;

    /**
     * @test
     */
    public function itCanUpdateTransactions()
    {
        $transaction = factory('App\Transaction')->create();
        $newTransaction = factory('App\Transaction')->make();

        $this->put('/transactions/' . $transaction->id, $newTransaction->toArray())
            ->assertRedirect('/transactions');

        $this->get('/transactions')
            ->assertSee($newTransaction->description);
    }

}

```

> La différence entre create() et make()
>
> La méthode `create` crée une instance du model et l'enregistre en BDD avec la méthode `save` de Eloquent.
> Là où la méthode `make` crée seulement une instance.

Les étapes suivantes sont :
- ajouter la route
- modifier le controller

### Validation

Ajoutez la validation des données dans le controller et effectuez les différents tests comme pour l'ajout d'une Transaction.