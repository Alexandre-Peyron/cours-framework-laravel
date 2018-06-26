# Formulaire Transaction

Notre controller est fonctionnel. Notre model est quasi complet.

Nous pouvons créer le formulaire pour ajouter une transaction.

### Routing et HTML

Créons la nouvelle route :

```php
// routes/web.php
Route::get('/transactions/create', 'TransactionsController@create');
```

Ensuite le controller :

```
// app/Http/Controllers/TransactionsController.php
public function create()
{
    return view('transactions.create');
}
```

Puis la vue :

```blade
@extends('layouts/app')

@section('content')
    <div class="container">
        <div class="panel panel-default">
            <div class="panel-heading">
                Création Transaction
            </div>
            <div class="panel-body">
                <form action="/transactions" method="POST">
                    <div class="form-group">
                        <label for="description">Description</label>
                        <input type="text" name="description" class="form-control" value="{{ old('description') }}">
                    </div>
                    <div class="form-group">
                        <label for="amount">Montant</label>
                        <input type="text" name="amount" class="form-control" value="{{ old('amount') }}">
                    </div>
                    <div class="form-group">
                        <label for="category_id">Catégorie</label>
                        <select name="category_id" class="form-control">
                            <option value=""></option>
                            {{-- TODO foreach cateogry --}}
                        </select>
                    </div>
                    <button class="btn btn-success" type="submit">Sauvegarder</button>
                </form>
            </div>
        </div>
    </div>
@endsection
```

Ajoutez des seeders pour les catégories.

Complétez le controller et la vue pour afficher la liste des catégories.

Testez manuellement le formulaire et itérez jusqu'à ce qu'il fonctionne.
