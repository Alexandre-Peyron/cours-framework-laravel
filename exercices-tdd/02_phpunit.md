### PHPUnit

[PHPUnit](https://phpunit.de/) est un framework open source de tests unitaires dédié au langage de programmation PHP.

C'est cet outil que nous allons utiliser dans le cadre de notre projet TDD.

### Installation

Par défaut, le Bundle PHPUnit est déjà présent dans le vendor d'un projet Laravel.

Pour éxecuter les premiers tests, utilisez la commande suivante :

```bash
./vendor/bin/phpunit
```

Normalement, 2 premiers tests vont s'exécuter.

L'un des 2 sera toujours vrai. L'autre test si l'URL / existe.

Si une erreur est renvoyée, c'est que votre environnement de travail est mal configuré.

Ces deux tests se trouvent dans le dossier `tests` à la racine de votre projet. 

### Alias

Appeler phpunit à chaque fois depuis le vendor, n'est pas très pratique.

Deux solutions s'offrent à vous :
- créer un `alias` dans votre OS pour écourter l'appel.
- utiliser la version compilée (.phar)
- installer phpunit globalement

Voir la [documentation](https://phpunit.de/getting-started/phpunit-7.html) pour plus de précisions.