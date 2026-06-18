# Refactor simple

## Rôle du concept

Le refactor simple consiste à améliorer la structure d’un code existant sans changer son comportement.

Il sert à rendre le code plus lisible, plus testable et plus facile à modifier.

Les actions de base sont : extraire une fonction, réduire une fonction trop longue et supprimer la duplication.

## Exemples

Avant refactor :

```python
email = " CLIENT@EXAMPLE.COM "
email = email.strip().lower()
```

Après refactor :

```python
def normalize_email(raw_email: str) -> str:
    return raw_email.strip().lower()
```

Exemple de duplication :

```python
customer_email = customer_email.strip().lower()
admin_email = admin_email.strip().lower()
```

Refactor :

```python
customer_email = normalize_email(customer_email)
admin_email = normalize_email(admin_email)
```

## Erreur typique

Changer le comportement du code pendant le refactor.

Exemples :

* ajouter une nouvelle fonctionnalité en même temps ;
* modifier une règle métier sans le vouloir ;
* extraire une fonction avec un nom vague ;
* casser un cas limite déjà géré ;
* refactorer sans test ou sans vérifier le résultat.

## Règle à retenir

Refactorer = changer la structure, pas le comportement.

Avant de refactorer, il faut comprendre ce que le code fait déjà.

Une bonne extraction de fonction doit avoir :

* un nom clair ;
* une responsabilité unique ;
* des paramètres explicites ;
* un retour clair.

## Utilité en projet

Dans `data-contract-cli`, le refactor simple servira à éviter un gros script illisible.

Exemples :

* extraire `normalize_email`;
* extraire `parse_date`;
* extraire `validate_required`;
* extraire `validate_row`;
* extraire `write_error_report`;
* séparer validation, transformation et écriture des fichiers.

Le refactor permettra de garder le moteur de validation lisible, testable et défendable à l’oral.
