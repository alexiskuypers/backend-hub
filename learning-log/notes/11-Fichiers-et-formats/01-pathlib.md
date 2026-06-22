# `pathlib`

## Rôle du concept

`pathlib` permet de représenter et manipuler les chemins de fichiers avec des objets `Path`.

Il évite de construire les chemins manuellement avec des chaînes de caractères et rend le code plus lisible et portable.

## Exemples

```python
from pathlib import Path

input_path = Path("data") / "invoices.csv"
```

Informations utiles :

```python
input_path.name      # "invoices.csv"
input_path.stem      # "invoices"
input_path.suffix    # ".csv"
input_path.parent    # Path("data")
```

Vérification d’un chemin :

```python
if not input_path.exists():
    raise FileNotFoundError(f"File not found: {input_path}")

if not input_path.is_file():
    raise ValueError(f"Expected a file: {input_path}")
```

Création d’un dossier de sortie :

```python
output_dir = Path("reports")
output_dir.mkdir(parents=True, exist_ok=True)
```

## Erreur typique

Construire les chemins avec des chaînes :

```python
output_path = "reports/" + filename
```

Cela devient fragile selon le système d’exploitation et la structure du chemin.

Autres erreurs fréquentes :

* confondre chemin relatif et chemin absolu ;
* supposer qu’un fichier ou dossier existe ;
* oublier de créer le dossier de sortie ;
* convertir trop tôt un objet `Path` en `str`.

## Règle à retenir

Utiliser des objets `Path` pour manipuler les chemins.

```python
path = directory / filename
```

Vérifier le chemin avant de l’utiliser et créer explicitement les dossiers nécessaires.

Convertir en `str` uniquement lorsqu’une bibliothèque l’exige.

## Utilité en projet

Dans `data-contract-cli`, `pathlib` permet de gérer proprement :

* le chemin du CSV d’entrée ;
* le chemin du contrat YAML ;
* le dossier de sortie ;
* les fichiers CSV, JSON et HTML générés ;
* la vérification de l’existence des fichiers ;
* la création des dossiers de rapports.

Exemple :

```python
clean_csv_path = output_dir / f"{input_path.stem}_clean.csv"
error_csv_path = output_dir / f"{input_path.stem}_errors.csv"
summary_path = output_dir / f"{input_path.stem}_summary.json"
```

Cela rend les chemins plus sûrs, lisibles et faciles à tester.
