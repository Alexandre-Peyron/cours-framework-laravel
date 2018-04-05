# Eloquent Relations

La documentation pour les relations est [ici](https://laravel.com/docs/master/eloquent-relationships).

L'objectif est de comprendre et mettre en place les relations entre les models Laravel.


### OneToMany - Model Comment

Nous allons créer un nouveau modèle `Comment` (Commentaire).
- title
- content
- created_at
- updated_at


Un article peut avoir plusieurs commentaires, un commentaire est associé à un seul article.

Dans l'ordre, il faut donc :
- créer la migration
- créer le model
- mettre à jour les 2 model (Article et Comment) pour créer la relation
- créer de nouveaux seeders.

Une fois vos modèles et données en place, modifiez la vue article.show afin d'afficher les commentaires.


### ManyToMany - Model Tag

Même travail que précédemment, pour le un modèle Tag, associé aux articles.