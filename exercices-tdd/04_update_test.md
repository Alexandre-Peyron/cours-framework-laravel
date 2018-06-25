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