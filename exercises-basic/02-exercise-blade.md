# Utilisation de Twig

Première chose à faire, comme toujours, ouvrir la [documentation](https://laravel.com/docs/5.6/blade) !

Le but de l'exercice est de comprendre les bases de blade: héritage, inclusion, gestion des blocs. 


### Les bases - Héritage

- Créez dans `resources/views` un nouveau template `layout.blade.php`

```blade
<html>
    <head>
        <title>Blog - @yield('title')</title>
    </head>
    <body>
        @section('sidebar')
            This is the master sidebar.
        @endsection

        <div class="container">
            @yield('content')
        </div>
    </body>
</html>
```

Plusieurs éléments à retenir ici :
- la directive `@section`, comme son nom l'indique, crée une nouvelle section. Directement utilisable dans layout mais également dans les templates enfants.
- la directive `@yield`, crée une nouvelle section utilisable que par les enfants. Cela permet, de se rendre compte tout de suite, visuellement de quels éléments devront être hériter obligatoirement.

A présent, déplacez les vues "article" précédemment créées, dans un dossier `resources/views/article`. 
Faites en sorte qu'elles héritent de notre layout.


### Les base - Inclusion

Télécharger un template de site tout prêt. Des exemples [ici](https://startbootstrap.com/template-categories/all/) avec bootstrap.

Mettez en place le template.

> Les fichiers JS et CSS sont à placer pour le moment dans `/public`.
> On approfondira par la suite la gestion des assets avec Webpack

Il faut que votre layout soit le plus plus lisible possible. 
Autrement dit, vous allez devoir découper le template en différents blocs (par exemple: header, menu, footer)
qui seront inclus dans votre layout.
 
