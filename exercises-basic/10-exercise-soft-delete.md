# Soft Delete

La documentation pour le soft delete est [ici](https://laravel.com/docs/5.6/eloquent#soft-deleting).

> Le soft delete consister à supprimer un élément tout en le conservant en base de données.
> Pour cela, nous allons ajouter une propriété à nos models (deleted_at) qui indique la date de suppression.

### Mise en place

Nous allons modifier notre model Comment

Ajoutez le trait dans le model :

```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;

class Comment extends Model
{
    use SoftDeletes; //Trait php

    /**
     * The attributes that should be mutated to dates.
     *
     * @var array
     */
    protected $dates = ['deleted_at'];
}
```

Créez une nouvelle migration

```php
Schema::table('flights', function ($table) {
    $table->softDeletes();
});
```

### Interface

Dans la page article.show, modifiez la liste des commentaires.

Ajouter un bouton "supprimer mon commentaire" pour les commentaires qui appartienne 
à l'utilisateur actuellement connecté.

Créez l'action de controller correspondante. Vérifiez bien que le commentaire à supprimer appartient bien à l'utilisateur connecté.