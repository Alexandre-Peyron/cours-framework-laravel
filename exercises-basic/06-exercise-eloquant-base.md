# Eloquent

Go sur la [doc](https://laravel.com/docs/master/eloquent).

Eloquent est l'ORM de Laravel.

> ORM (Object Relational Mapping) : 
> Un ORM est un outil d'abstraction de base de données. C'est une surcouche facilitant l'utilisation et les requêtes SQL.
> Pour faire simple, cela signifie qu'une table dans votre base de données va correspondre à une class dans votre langage de programmation (PHP, Java...) et inversement.

### Index

Nous allons maintenant remplir l'action `index` du controller et créer une vue associée si ce n'est pas déjà fait.

Commencez par afficher simplement la liste de tous les articles.

Dans un deuxième temps, affichez seulement ceux dont is_enabled = true.

Et dans un dernier temps, ordonnez les par date de création. Le plus récent en haut de la liste.

Sur chaque élément de la liste, ajoutez un lien pour accéder à la vue "show" d'un article.


### Show

Ici, nous allons afficher le contenu d'un article en fonction de l'ID passer en paramètre.

Si l'article est is_enabled = false, rediriger vers l'index.

Une fois tout ça en place, on va maintenant modifier notre table articles.

Créez une nouvelle migration, pour ajouter une propriété `slug` (string) à notre article.
Modifiez ensuite les seeds (str_slug()).

> Dans notre cas, le slug correspond au titre de l'article mais optimisé pour être utilisé dans une URL.
> Exemple : "Mon titre génial" devient "mon-titre-genial". 
> On supprime donc les espaces, accents et majuscules.

Modifiez à présent les liens dans l'index ainsi que la fonction show, pour que vos URLs soient toutes belles !


