# Fonctions

## Rôle du concept

Une fonction permet de découper une logique en petite unité réutilisable, lisible et testable.

Elle reçoit des entrées, applique une logique précise, puis retourne un résultat.

## Exemples

```python
def normalize_email(raw_email: str) -> str:
    return raw_email.strip().lower()
```

```python
email = normalize_email(" CLIENT@EXAMPLE.COM ")
print(email)  # client@example.com
```

## Erreurs typiques

Écrire une fonction qui fait trop de choses à la fois.

Exemple mauvais : lire un fichier, nettoyer les données, afficher le résultat et écrire un rapport dans une seule fonction.

Autre erreur : utiliser `print()` au lieu de `return`, ce qui rend la fonction difficile à tester.

## Règles à retenir

Une bonne fonction doit avoir une responsabilité claire.

Entrée claire → traitement clair → sortie claire.

Si une fonction devient difficile à nommer, c’est souvent qu’elle fait trop de choses.

## Utilité en projet

Dans `data-contract-cli`, les fonctions doivent isoler les traitements testables :

* parser une date ;
* normaliser un email ;
* valider un montant ;
* vérifier une règle ;
* construire une erreur ligne par ligne.

Objectif : pouvoir tester la logique sans lire ni écrire de vrais fichiers.
