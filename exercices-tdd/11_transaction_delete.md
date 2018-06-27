# Supprimer une transaction

### Test

Créez un nouveau fichier pour tester le `delete` d'une transaction.

```bash
php artisan make:test DeleteTransactionTest
```

```php
/**
 * @test
 */
public function itCanDeleteTransaction()
{
    $transaction = factory('App\Transaction')->create();

    $this->delete('/transactions/'. $transaction->id)
        ->assertRedirect('/transactions');

    $this->get('/transactions')
        ->assertDontSee($transaction->description);
}
```

Effectuez les évolutions de code nécessaire pour que le test passe au vert.


### HTML

Maintenant que la route et le controller sont à jour, 
nous pouvons ajouter un bouton pour supprimer une transaction dans notre projet.

Dans le fichier `resources > views > transactions > index`, ajoutons une nouvelle case au tableau ainsi qu'un formulaire de suppression.

```blade
<td>
    <form action="/transactions/{{$transaction->id}}" method="POST">
        {{ method_field('DELETE') }}
        {{ csrf_field() }}
        <button class="btn btn-danger btn-xs" type="submit" >Supprimer</button>
    </form>
</td>
```

Testez manuellement.

Voilà, les actions de bases (CRUD) d'un model sont en place avec les tests associés.