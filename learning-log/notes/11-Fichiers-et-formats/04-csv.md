# CSV réel

## Rôle du concept

Un CSV réel peut être techniquement lisible tout en contenant des imperfections :

* séparateur différent de celui attendu ;
* en-têtes obligatoires absents ;
* colonnes supplémentaires ;
* lignes trop courtes ou trop longues ;
* cellules vides ;
* valeurs impossibles à convertir ;
* données ne respectant pas les règles métier.

Le programme doit distinguer :

```text
erreur globale du fichier
→ le traitement normal ne peut pas commencer ou continuer

erreur locale à une ligne
→ la ligne est rejetée, mais les autres peuvent être traitées
```

L’objectif n’est pas de réparer tous les CSV possibles, mais de :

* corriger les problèmes déterministes ;
* détecter les anomalies ;
* isoler les lignes invalides ;
* refuser les fichiers trop ambigus ;
* ne jamais inventer de données.

## Lecture avec paramètres explicites

```python
import csv

with input_path.open(
    "r",
    encoding="utf-8-sig",
    newline="",
) as file:
    reader = csv.DictReader(
        file,
        delimiter=";",
    )
```

Le séparateur et l’encodage doivent être connus, configurés ou déterminés selon une politique claire.

Utiliser le mauvais séparateur peut conduire à interpréter :

```text
id;name;age
```

comme une seule colonne.

## Vérification de la structure globale

```python
required_columns = {
    "invoice_id",
    "amount",
    "invoice_date",
}

received_columns = set(reader.fieldnames or [])

missing_columns = required_columns - received_columns
extra_columns = received_columns - required_columns
```

Si une colonne obligatoire manque :

```python
if missing_columns:
    raise MissingRequiredColumnError(
        f"Missing required columns: {sorted(missing_columns)}"
    )
```

Il s’agit généralement d’une erreur globale, car aucune ligne ne peut respecter complètement le contrat attendu.

Les colonnes supplémentaires peuvent être :

* refusées ;
* acceptées ;
* ignorées ;
* signalées par un warning.

Cette décision dépend du contrat de l’application.

## Validation de chaque ligne

```python
valid_rows = []
error_rows = []

for row_number, row in enumerate(reader, start=2):
    try:
        cleaned_row = validate_row(row)
    except RowValidationError as error:
        error_rows.append(
            {
                "row_number": row_number,
                "record_id": row.get("invoice_id"),
                "field": error.field,
                "raw_value": error.raw_value,
                "error": str(error),
            }
        )
        continue

    valid_rows.append(cleaned_row)
```

Une erreur applicative locale ne doit pas nécessairement arrêter tout l’import.

Un bug inattendu ne doit pas être capturé comme une simple erreur de ligne.

## Ligne trop longue

Avec `DictReader`, les valeurs supplémentaires sont généralement rangées sous la clé `None`.

```python
if None in row:
    extra_values = row[None]

    raise RowValidationError(
        "row contains too many values",
        field="__row__",
        raw_value=extra_values,
    )
```

Exemple :

```python
{
    "invoice_id": "INV-001",
    "amount": "50",
    "invoice_date": "2026-06-01",
    None: ["EXTRA"],
}
```

## Ligne trop courte

Une valeur correspondant à une cellule absente est généralement représentée par `None`.

```python
missing_fields = [
    field
    for field, value in row.items()
    if field is not None and value is None
]
```

Il faut distinguer :

```text
None
→ cellule absente parce que la ligne est trop courte

""
→ cellule présente mais vide
```

Exemple :

```csv
INV-001;50
```

La troisième cellule est absente.

```csv
INV-001;50;
```

La troisième cellule existe mais elle est vide.

## Donnée brute, nettoyage et conversion

La donnée brute doit être conservée avant toute transformation.

```python
raw_amount = row.get("amount")

cleaned_amount = (
    raw_amount.strip()
    if raw_amount is not None
    else None
)
```

Puis :

```text
donnée brute
→ nettoyage
→ conversion
→ validation métier
```

Exemple :

```text
" 50 "
→ "50"
→ 50
→ montant valide
```

Le rapport d’erreurs conserve la valeur brute afin de montrer exactement ce qui a été reçu.

## Erreurs globales

Exemples :

* fichier absent ;
* encodage incompatible ;
* séparateur incompatible avec le contrat ;
* en-tête absent ;
* colonne obligatoire manquante ;
* syntaxe CSV suffisamment corrompue pour empêcher une lecture fiable.

Décision :

```text
arrêter l’import
→ lever une exception applicative claire
→ produire un message utilisateur
→ logger l’échec
→ retourner un exit code approprié
```

## Erreurs locales

Exemples :

* cellule obligatoire vide ;
* ligne trop courte ;
* valeur supplémentaire ;
* type invalide ;
* valeur hors limites ;
* règle métier non respectée.

Décision habituelle :

```text
rejeter la ligne
→ enregistrer une erreur structurée
→ continuer avec la ligne suivante
```

## Règle à retenir

Avant de valider les données :

1. ouvrir le fichier avec un encodage explicite ;
2. utiliser le séparateur attendu ;
3. vérifier les en-têtes ;
4. vérifier les colonnes obligatoires ;
5. choisir une politique pour les colonnes inconnues.

Ensuite, pour chaque ligne :

1. conserver les valeurs brutes ;
2. détecter les cellules absentes ou supplémentaires ;
3. nettoyer les valeurs ;
4. convertir les types ;
5. appliquer les règles métier ;
6. conserver la ligne valide ou enregistrer ses erreurs.

## Utilité dans `data-contract-cli`

Le contrat YAML définit notamment :

```yaml
encoding: "utf-8"
delimiter: ","

columns:
  invoice_id:
    required: true

  amount:
    required: true
    type: decimal
```

L’outil doit :

* refuser un fichier globalement incompatible avec son contrat ;
* ne pas tenter de réparer une structure ambiguë ;
* gérer les colonnes inconnues selon la politique choisie ;
* valider les lignes séparément ;
* conserver les lignes valides ;
* produire un fichier propre ;
* produire un rapport détaillé des erreurs.

L’objectif est de transformer un CSV structurellement lisible mais imparfait en sorties fiables, sans masquer les problèmes ni inventer de données.
