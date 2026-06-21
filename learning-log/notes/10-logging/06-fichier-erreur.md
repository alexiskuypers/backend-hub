# Rapport d’erreurs

Un rapport d’erreurs est une sortie métier qui liste les données rejetées pendant un traitement.

Il ne remplace pas les logs.

## Différence avec `app.log`

### `app.log`

Le fichier de logs décrit le déroulement du programme :

* démarrage du traitement ;
* fichier chargé ;
* nombre de lignes lues ;
* étape terminée ;
* avertissement ;
* échec technique ;
* fin du traitement.

Exemple :

```text
INFO | Processing started: file=customers.csv
INFO | Validation completed: valid=950 invalid=50
INFO | Error report written: file=errors.csv
INFO | Processing completed
```

### Rapport d’erreurs

Le rapport indique quelles données sont invalides et pourquoi.

Exemple :

```csv
row_number,record_id,field,raw_value,error
12,C-004,age,abc,invalid integer
19,C-011,email,test,invalid email
27,C-018,quantity,-3,must be positive or zero
```

Il peut contenir :

* le numéro de ligne ;
* l’identifiant de l’enregistrement ;
* le champ concerné ;
* la valeur brute ;
* le type ou message d’erreur.

## Quand en créer un ?

Créer un rapport d’erreurs lorsque :

* plusieurs données peuvent être invalides ;
* le traitement continue malgré certaines erreurs ;
* l’utilisateur doit pouvoir corriger les données ;
* mettre chaque détail dans les logs produirait trop de bruit.

## Règle simple

Un problème de fonctionnement du programme va dans les logs.

Une donnée invalide à corriger va dans le rapport d’erreurs.

Création = deux listes, une pour ligne valide, l'autre pour ligne invalide, remplissage pendant le traitement puis création du fichier et insertion des listes.

## Organisation générale

```text
input.csv
    ↓
traitement
    ├── app.log      → déroulement du programme
    ├── clean.csv    → données valides
    └── errors.csv   → données invalides et raisons
```

Une ligne invalide n’a pas besoin d’être détaillée intégralement dans `app.log`.

Le log peut seulement résumer :

```text
WARNING | Validation completed with invalid rows: valid=950 invalid=50
```

Les cinquante erreurs détaillées restent dans `errors.csv`.
