# Orchestration

## Rôle du concept

L’orchestration consiste à coordonner les étapes du programme dans le bon ordre.

Une fonction d’orchestration ne doit pas contenir toute la logique métier. Elle doit appeler les bonnes fonctions au bon moment.

Elle sert à rendre le flux général du programme clair et lisible.

## Exemples

```python
def run_validation(input_path, contract_path, output_paths):
    contract = load_contract(contract_path)
    validate_contract(contract)

    rows = read_csv(input_path)
    result = validate_rows(rows, contract)

    write_clean_csv(result.valid_rows, output_paths.clean_csv)
    write_error_report(result.errors, output_paths.error_csv)
    write_summary(result.summary, output_paths.summary_json)

    return result.exit_code
```

Cette fonction orchestre le traitement.

Elle ne contient pas les détails de lecture, de parsing, de validation ou d’écriture. Elle coordonne les étapes.

## Erreur typique

Mettre toute l’application dans une énorme fonction `run()` ou `main()`.

Exemples :

* parser les arguments CLI dans la même fonction que la validation ;
* lire le CSV, valider les lignes et écrire les rapports dans un seul bloc ;
* mettre de la logique métier directement dans l’orchestrateur ;
* avoir plusieurs points d’entrée flous dans le programme.

## Règle à retenir

L’orchestrateur décrit le scénario général.

Il répond à la question : “dans quel ordre les étapes doivent-elles se produire ?”

Il coordonne, mais ne fait pas le travail détaillé à la place des fonctions spécialisées.

## Utilité en projet

Dans `data-contract-cli`, l’orchestration doit suivre ce flux :

* lire les arguments CLI ;
* charger le contrat YAML ;
* valider le contrat ;
* lire le CSV ;
* valider les lignes ;
* séparer les lignes valides et invalides ;
* écrire le CSV propre ;
* écrire le rapport d’erreurs ;
* écrire le résumé JSON ;
* retourner le bon exit code.

Cette orchestration rend le programme compréhensible, testable et défendable à l’oral.
