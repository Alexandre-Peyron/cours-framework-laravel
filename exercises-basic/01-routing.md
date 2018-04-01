# Routing

Premier réflexe : la [documentation](https://laravel.com/docs/master/routing) 

L'objectif de cet exercice est de comprendre la mise en place et génération des routes avec Laravel
ainsi que la création des views.

> **Une route** : c'est le chemin/URL vers votre page.

> **Une view** : elle correspond à l'affichage de votre page.


### Route de base

Pour commencer, nous allons travailler dans le fichier `routes/web.php`.

> Ce fichier web.php contiendra toutes vos routes qui concernent l'interface web.
 
> On verra par la suite comment mieux organiser nos routes avec la gestion des controllers mais ce n'est pas l'objectif ici.

Une première route est présente dans le fichier. C'est celle qui affiche la page par défaut de Laravel

```php
Route::get('/', function () {
    return view('welcome');
});
```

Pour explication, la fonction static `Route::get` crée une nouvelle route avec pour méthode GET.
En toute logique `Route::post` créerait une route en POST. En toute logique `Route::put`...

La fonction prend 2 paramètres. D'une part, l'url de la route. Ici `/`.

D'autre part, une fonction anonyme qui correspond à l'action de notre route.

Celle-ci est assez permissive car on peut retourner une view, un array, une variable.

Dans notre cas, elle retourne une view avec un nom de template. Ce template se trouve dans `resources/views/welcome.blade.php`.


Votre travail maintenant est de créer une nouvelle route `/articles` qui affiche une liste de titres d'articles.

```php
// Placez ce tableau au début de votre action de controller
$articles = [
    "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
    "Vivamus id massa ac ex rutrum vestibulum."
    "Nam purus justo, porttitor vel urna id, blandit aliquam orci."
]
```


### Paramètres

Il est évidemment possible d'avoir des paramètres dynamiques au sein d'une route.

Créez à présent une nouvelle route `/article/{index}` qui va afficher l'index du tableau précedent.

Différentes contraintes à ajouter ensuite :
    - `index` doit être un nombre
    - si l'index n'existe pas, rediriger vers `/articles`
    - donner une nom à la route
    
    
### Paramètres avancés

Nouveau tableau d'articles :

```php
// Placez ce tableau au début de votre action de controller
$articles = [
    [
        "title" => "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
        "year" => 2018,
        "tags" => ["Lorem", "Ipsum"]
    ],
    [
        "title" => "Vivamus id massa ac ex rutrum vestibulum.",
        "year" => 2018,
        "tags" => ["Lorem", "Massa"]
    ],
    [
        "title" => "Nam purus justo, porttitor vel urna id, blandit aliquam orci.",
        "year" => 2017,
        "tags" => ["Ipsum", "Massa"]
    ],
]
```

Créez à présent une nouvelle route `/articles/{year}/{tag}` dont `year` et `tag` sont optionnels.

Le but étant de filtrer les articles en fonction de l'année et/ou du tag renseigné(s) et d'afficher la liste correspondante.


