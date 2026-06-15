# Imports propres

## Rôle du concept

Les imports permettent d’utiliser du code défini dans un autre module.

Des imports propres rendent le projet lisible et évitent les dépendances confuses entre fichiers.

## Exemples

```python
from data_contract.transforms import normalize_email
from data_contract.validators import validate_decimal
```

Exemple mental :

```text
main.py importe les modules spécialisés
les modules spécialisés ne doivent pas dépendre de main.py
```

## Erreurs typiques

Créer un import circulaire.

Exemple :

```text
a.py importe b.py
b.py importe a.py
```

Autre erreur : mettre du code exécuté directement au niveau du module.

```python
print("Traitement lancé")  # exécuté dès l'import
```

## Règles à retenir

Importer un module exécute son code de haut niveau.

Donc un module doit surtout contenir :

* fonctions ;
* classes ;
* constantes ;
* définitions.

Le code de lancement doit être protégé avec :

```python
if __name__ == "__main__":
    main()
```

## Utilité en projet

Dans `data-contract-cli`, les imports propres évitent que la lecture du CSV, la validation ou les rapports se lancent simplement parce qu’un fichier est importé.

Le CLI doit orchestrer.

Les modules métier doivent fournir des fonctions testables, sans effet caché au moment de l’import.
