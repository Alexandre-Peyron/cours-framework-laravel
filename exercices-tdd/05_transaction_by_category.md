# Lister les transactions par catégorie

A présent, l'objectif est d'ajouter un paramètre optionnel à notre route existante,
pour n'afficher que les transactions dont la catégorie est en paramètre.

### Test

Créons un nouveau test dans notre fichier `test > Features > ViewTransactionsTest.php`

```php
/**
 * @test
 */
public function itCanFilterTransactionsByCategory()
{
    $category = factory('App\Category')->create();
    $transaction = factory('App\Transaction')->create(['category_id' => $category->id]);
    $otherTransaction = factory('App\Transaction')->create();

    $this->get('/transactions/' . $category->slug)
        ->assertSee($transaction->description)
        ->assertDontSee($otherTransaction->description);
}
```

### Controller

Modifions la route, pour rendre la catégorie optionnelle.

```php
//routes/web.php
Route::get('/transactions/{category?}', 'TransactionsController@index');
```

Puis l'action de controller :

```php
public function index(Category $category = null)
{
    if ($category && $category->exists) {
        $transactions = $transactions = Transaction::latest()->where('category_id', $category->id)->get();
    }
    else {
        $transactions = Transaction::latest()->get();
    }

    return view('transactions.index', compact('transactions'));
}
```

### Slug

Mettons en place le slug des catégories pour avoir une URL fonctionnelle.

> Le slug est un champ unique d'un model compatible pour les URLs. C'est à dire, sans espace, accent ou caractères spéciaux.

Première étape, la migration : `$table->string('slug');`

Deuxièmement le model :

```php
public function getRouteKeyName()
{
    return 'slug';
}
```

Et en troisième temps, la factory :

```php
$factory->define(App\Category::class, function (Faker $faker) {
    $name = $faker->word;
    
    return [
        'name' => $name,
        'slug' => str_slug($name),
    ];
});
```

A présent, le test doit être fonctionnel.