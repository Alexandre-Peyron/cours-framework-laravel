# Connexion utilisateur

La documentation pour la connexion est [ici](https://laravel.com/docs/5.6/authentication).

L'objectif est de comprendre et mettre en place la connexion utilisateur.

### Installation

Par chance, tout est déjà intégré dans Laravel.

Utilisez la commande suivate :

```bash
php artisan make:auth
```

C'est tout pour moi. Merci aurevoir.


Dans le détail, plusieurs fichiers ont été générés : 
- resources/views/auth
- resources/views/layouts
- app/Http/Controllers/Auth
- le fichier routes/web.php a été modifié


A présent, modifiez vos views pour qu'elles héritent de `layout.app` et ainsi avoir un header avec les liens de connexion et inscription.

Testez l'inscription, puis la connexion.


### Commentaire

Modifiez la page article.show, en faisant en sorte que le formulaire d'ajout de commentaire 
ne soit visible que lorsque l'utilisateur est connecté.

A l'ajout d'un commentaire, dans l'action de controller correspondante, associé l'utilisateur actuellement connecté à ce nouveau commentaire.