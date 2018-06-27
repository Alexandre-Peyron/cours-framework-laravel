# Template Mise à jour Transaction

A présent, travaillons sur la view du formulaire d'update.

Dans l'ordre, il faut :

- ajouter la route
- ajouter l'action de controller
- créer la view (ci dessous)

```blade
@extends('layouts/app')

@section('content')
    <div class="container">
        <div class="panel panel-default">
            <div class="panel-heading">
                Création Transaction
            </div>
            <div class="panel-body">
                <form action="/transactions/{{ $transaction->id }}" method="POST">
                    {{ method_field('PUT') }}
                    {{ csrf_field() }}
                    <div class="form-group {{ $errors->has('description') ? 'has-error' : '' }}">
                        <label for="description">Description</label>
                        <input type="text" name="description" class="form-control" value="{{ old('description') ?: $transaction->description }}">
                    </div>
                    <div class="form-group {{ $errors->has('amount') ? 'has-error' : '' }}">
                        <label for="amount">Montant</label>
                        <input type="text" name="amount" class="form-control" value="{{ old('amount') ?: $transaction->amount }}">
                    </div>
                    <div class="form-group {{ $errors->has('category_id') ? 'has-error' : '' }}">
                        <label for="category_id">Catégorie</label>
                        <select name="category_id" class="form-control">
                            @foreach($categories as $category)
                                <option value="{{ $category->id }}" {{ $category->id == (old('category_id') ?: $transaction->category_id) ?  'selected' : '' }} >
                                    {{ $category->name }}
                                </option>
                            @endforeach
                        </select>
                    </div>
                    <button class="btn btn-success" type="submit">Mettre à jour</button>
                </form>
            </div>
        </div>
    </div>
@endsection
```

Testez manuellement le fonctionnement.


Améliorez votre interface pour la rendre plus utilisable (menu dans le header, lien entre les pages...).
