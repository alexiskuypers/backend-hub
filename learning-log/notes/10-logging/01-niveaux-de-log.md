# Niveaux de logs

## Rôle du concept

Les niveaux de logs indiquent la gravité et l’utilité d’un message.

Ils permettent de distinguer une information de diagnostic, une exécution normale, un problème évitable ou une erreur réelle.

## Exemples

```python
import logging

logger = logging.getLogger(__name__)

logger.debug("Parsed value: %r", raw_value)
logger.info("Validation started for file: %s", input_path)
logger.warning("Unknown column ignored: %s", column_name)
logger.error("Unable to read input file: %s", input_path)
```

Dans un bloc `except` :

```python
try:
    content = input_path.read_text(encoding="utf-8")
except OSError:
    logger.exception("Unable to read input file: %s", input_path)
    raise
```

## Erreur typique

Utiliser le mauvais niveau.

Exemples :

* tout enregistrer en `info` ;
* utiliser `error` pour un simple avertissement ;
* utiliser `exception` en dehors d’un bloc `except` ;
* logger deux fois la même erreur à plusieurs niveaux ;
* enregistrer chaque ligne CSV et rendre les logs illisibles.

## Règle à retenir

* `debug` : détails techniques utiles pendant le développement, ajouter %r ;
* `info` : étapes normales et importantes du programme ;
* `warning` : problème non bloquant ou situation inhabituelle ;
* `error` : échec connu, sans afficher automatiquement la traceback ;
* `exception` : erreur capturée dans un `except`, avec traceback.

```text
debug < info < warning < error
```

`logger.exception()` s’utilise uniquement pendant la gestion d’une exception.

## Utilité en projet

Dans `data-contract-cli` :

* `debug` → valeur parsée, règle appliquée, détail technique ;
* `info` → début du traitement, fichiers utilisés, nombre de lignes traitées ;
* `warning` → colonne inconnue acceptée en mode permissif ;
* `error` → contrat invalide ou fichier inaccessible avec message propre ;
* `exception` → erreur inattendue nécessitant la traceback pour être diagnostiquée.

Le niveau choisi doit permettre de comprendre l’exécution sans noyer les informations importantes.

## Placement stratégique :
DEBUG

À placer dans les fonctions techniques ou intermédiaires quand tu veux voir :

une valeur brute ;
une valeur transformée ;
une décision interne ;
un compteur intermédiaire ;
les paramètres techniques utiles.
logger.debug("Parsing quantity: raw_value=%r", raw_value)

À éviter : logger chaque ligne de code.

INFO

À placer surtout dans l’orchestration pour suivre :

le début d’un traitement ;
la fin d’un traitement ;
une étape importante terminée ;
le nombre d’éléments traités ;
un succès global.
logger.info("Processing started: row_count=%d", len(rows))

À éviter : un log INFO dans chaque petite fonction.

WARNING

À placer à l’endroit où le programme détecte une situation inhabituelle mais récupérable :

élément ignoré ;
valeur par défaut utilisée ;
tentative supplémentaire ;
donnée optionnelle anormalement absente ;
résultat partiel.
logger.warning("Row skipped: row_number=%d", row_number)
ERROR

À placer au niveau qui constate l’échec final d’une opération :

traitement impossible ;
fichier obligatoire absent ;
aucune donnée valide ;
erreur applicative prévue ;
commande qui doit se terminer en échec.
logger.error("Processing failed: no valid rows")

Souvent dans l’orchestration ou le point d’entrée.

EXCEPTION

À placer uniquement dans un except quand la traceback aide réellement :

erreur imprévue ;
enchaînement complexe ;
bug difficile à localiser ;
appel externe ayant échoué sans cause évidente.
except AppError:
    logger.exception("Import failed")
    raise
