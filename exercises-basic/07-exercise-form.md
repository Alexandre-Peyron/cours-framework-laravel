# Formulaire

La documentation pour la validation des formulaires est [ici](https://laravel.com/docs/master/validation).

L'objectif est de créer et valider les formulaire avec Laravel.

### Create

La première étape consiste à compléter l'action `create` de notre controler.
Celle-ci sert juste à afficher un formulaire.

- Créez une nouvelle vue `article.create`.
- Y intégrer un formulaire HTML. 
    - L'action du formulaire doit correspondre à la méthode `store` de votre controller et la méthode POST.
    - Attention, le `name` des champs doit correspondre aux propriétés de votre Article.
    - La validation du formulaire nécessite l'utilisation de `@csrf` pour protéger votre form. 


### Store

Nous allons maintenant soumettre et valider le formulaire dans la méthode `store` de notre controller.

Commencez par mettre, la ligne suivante dans l'action du controller pour voir ce qui est envoyé à la soumission du form.

```php
<?php

dd($request->all());

```

Pour soumettre les données du form, la méthode la plus simple est la suivante :

```php
<?php

Article::create($request->all());
```

Ajoutez une redirection vers la page de l'Article nouvellement créé. Testez si tout est fonctionnel.

Malheureusement, cette méthode de valide pas les données rentrées.
Pour ce faire, il faut utiliser le validateur et définir pour chaque propriété du model, les règles à appliquer.

```php
<?php

$validator = Validator::make(request(), [
    'title'   => 'required|unique:articles|max:100',
    'content' => 'required'
]);

if ($validator->fails()) {
    return redirect('articles/create')
                ->withErrors($validator)
                ->withInput();
}

```

Ajoutez [l'affichage des erreurs](https://laravel.com/docs/master/validation#working-with-error-messages) dans le formulaire.