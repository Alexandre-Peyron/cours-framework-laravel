# Montant d'une transaction

Il y a une propriété que nous avons oublié de mettre dans notre model transaction : Le montant `amount`.

Ajoutez la dans la migration et effectuez l'ensemble des tests.

Normalement, plusieurs d'entre eux doivent passer en erreur.

> Le mise en place des tests sert exactement pour ce cas de figure. 
>
> On modifie une entité/model/class existante et grâce aux tests on a un rendu direct de l'impact de cette modification.

Corrigez le code pour que les tests soient de nouveau bons.
- model
- factory
- view

Ajoutez 2 tests pour le montant :
- amount = null
- amount = 'abc' 
