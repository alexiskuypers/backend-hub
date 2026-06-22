# Sorties propres

## Rôle du concept

Les sorties propres permettent de séparer les données exploitables des données invalides.

Le programme produit au minimum :

* un fichier de résultat avec les lignes valides ;
* un rapport d’erreurs avec les lignes ou valeurs rejetées.

Les fichiers doivent être lisibles, prévisibles et directement utilisables.

## Exemples

Écriture du fichier de résultat :

```python
with clean_path.open("w", encoding="utf-8", newline="") as file:
    writer = csv.DictWriter(file, fieldnames=column_names)
    writer.writeheader()
    writer.writerows(valid_rows)
```

Écriture du rapport d’erreurs :

```python
error_columns = [
    "row_number",
    "column",
    "error_code",
    "message",
]

with error_path.open("w", encoding="utf-8", newline="") as file:
    writer = csv.DictWriter(file, fieldnames=error_columns)
    writer.writeheader()
    writer.writerows(validation_errors)
```

## Erreur typique

* mélanger les lignes valides et invalides dans le même fichier ;
* afficher les erreurs uniquement dans le terminal ;
* produire des fichiers sans en-têtes ;
* écraser le fichier d’entrée ;
* utiliser des noms de sortie imprévisibles ;
* écrire un rapport sans numéro de ligne ni colonne concernée ;
* générer un fichier partiel après un échec d’écriture.

## Règle à retenir

Chaque sortie doit avoir un rôle clair.

```text
données valides → fichier de résultat
données invalides → rapport d’erreurs
résumé global → JSON ou affichage CLI
```

Le rapport d’erreurs doit indiquer au minimum :

* la ligne concernée ;
* la colonne concernée ;
* un code d’erreur ;
* un message utile.

Le fichier d’entrée ne doit jamais être modifié.

## Utilité en projet

Dans `data-contract-cli`, une validation peut produire :

```text
reports/invoices_clean.csv
reports/invoices_errors.csv
reports/invoices_summary.json
```

Le CSV propre contient uniquement les lignes valides et normalisées.

Le rapport d’erreurs permet de retrouver précisément ce qui doit être corrigé.

Exemple :

```csv
row_number,column,error_code,message
3,amount,INVALID_DECIMAL,"'abc' is not a valid decimal"
4,invoice_date,INVALID_DATE,"'wrong-date' does not match an accepted format"
```

Ces sorties rendent le traitement vérifiable, automatisable et exploitable par un utilisateur ou un autre système.
