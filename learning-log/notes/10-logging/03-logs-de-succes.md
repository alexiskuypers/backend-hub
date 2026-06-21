# Logs de succès

## Rôle du concept

Les logs de succès indiquent quelles étapes importantes ont été terminées correctement.

Ils permettent de vérifier que le traitement est allé jusqu’au bout et de savoir ce qui a réellement été produit.

## Exemples

```python
logger.info(
    "Validation completed: file=%s total_rows=%d valid_rows=%d invalid_rows=%d",
    input_path.name,
    total_rows,
    valid_rows,
    invalid_rows,
)
```

```python
logger.info("Clean CSV written: path=%s", clean_output_path)
```

## Erreur typique

Écrire uniquement des logs d’erreur.

Sans logs de succès, on ne sait pas si :

* le fichier a bien été lu ;
* la validation s’est terminée ;
* les rapports ont été générés ;
* le programme est arrivé à la fin.

Il faut aussi éviter de logger chaque petite opération réussie, au risque de noyer les informations importantes.

## Règle à retenir

Logger les étapes importantes terminées, pas chaque instruction exécutée.

Un bon log de succès précise :

* ce qui a été terminé ;
* quelle donnée a été traitée ;
* quel résultat a été obtenu ;
* où la sortie a été écrite.

Le message de fin ne doit être enregistré que lorsque tout le traitement est réellement terminé.

## Utilité en projet

Dans `data-contract-cli`, les logs de succès peuvent indiquer :

* le contrat chargé et validé ;
* le CSV lu correctement ;
* le nombre de lignes traitées ;
* le nombre de lignes valides et invalides ;
* les fichiers de sortie générés ;
* la fin complète de l’exécution.

Exemple :

```text
Validation completed: file=invoices.csv total_rows=100 valid_rows=94 invalid_rows=6
```

Ces logs permettent de confirmer rapidement que le traitement a fonctionné et de retrouver les résultats produits.
