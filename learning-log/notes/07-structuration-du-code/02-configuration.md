# Configuration

## Rôle du concept

La configuration consiste à centraliser les valeurs qui peuvent changer selon l’environnement, la commande ou l’usage du programme.

Elle évite de coder en dur les chemins, les paramètres, les modes d’exécution, les niveaux de logs ou les variables d’environnement.

La configuration permet de garder le code métier stable, même si les options d’exécution changent.

## Exemples

```python
from pathlib import Path

DEFAULT_OUTPUT_DIR = Path("reports")
DEFAULT_ENCODING = "utf-8"
DEFAULT_MODE = "strict"
```

Exemple avec variable d’environnement :

```python
import os

LOG_LEVEL = os.getenv("LOG_LEVEL", "INFO")
```

Exemple avec une configuration reçue depuis la CLI :

```python
config = {
    "input_path": "data/input.csv",
    "contract_path": "contracts/invoices.yml",
    "mode": "strict",
    "output_dir": "reports",
}
```

## Erreur typique

Coder des chemins ou paramètres en dur directement dans la logique métier.

Exemples :

* écrire `/home/alex/project/data/input.csv` dans le code ;
* répéter `"utf-8"` dans plusieurs fichiers ;
* mettre le mode `strict` directement dans une fonction de validation ;
* disperser les paramètres dans tout le projet ;
* mélanger configuration et logique métier.

## Règle à retenir

Une valeur qui peut changer doit être centralisée.

Le code métier ne doit pas dépendre de chemins fixes ou de paramètres cachés.

La configuration prépare le programme.
La logique métier utilise les données déjà préparées.

## Utilité en projet

Dans `data-contract-cli`, la configuration peut gérer :

* le chemin du CSV d’entrée ;
* le chemin du contrat YAML ;
* le dossier de sortie ;
* l’encodage ;
* le mode `strict` ou `permissive`;
* le niveau de logs ;
* les chemins des rapports générés ;
* les valeurs nulles définies dans le contrat YAML.

Cette séparation rend l’outil plus clair, plus flexible et plus facile à lancer dans différents contextes.
