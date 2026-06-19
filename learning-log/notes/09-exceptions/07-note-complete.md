# Gestion d'erreurs Python — fiche décisionnelle courte

## Règle centrale

Une fonction basse ne cache pas une erreur.

Elle retourne un résultat, retourne `None`, ou lève une exception.

Une fonction haute décide quoi afficher, logger ou retourner comme code de sortie.

On attrape une erreur seulement si on sait quoi en faire.

---

## 1. Résultat normal

Situation : la fonction peut produire le résultat attendu.

Décision : retourner le résultat.

```python
def calculate_price(quantity: int, unit_price: float) -> float:
    if quantity < 0:
        raise ValueError(f"invalid quantity: {quantity}")

    return quantity * unit_price
```

Situation : la valeur est valide.

Décision : `return`.

Situation : la valeur rend le résultat faux.

Décision : `raise`.

Situation : retourner `0`, `""` ou `False` cacherait l'erreur.

Décision : ne pas inventer une valeur valide.

---

## 2. Absence normale

Situation : l'absence est un résultat possible.

Décision : retourner `None`.

```python
def find_book_by_id(book_id: str, books: list[dict[str, str]]) -> dict[str, str] | None:
    for book in books:
        if book.get("id") == book_id:
            return book

    return None
```

Situation : l'élément est trouvé.

Décision : retourner l'élément.

Situation : l'élément n'est pas trouvé.

Décision : retourner `None`.

Situation : le retour peut être absent.

Décision : annoter avec `| None`.

---

## 3. Erreur bloquante

Situation : la fonction ne peut pas respecter son contrat.

Décision : lever une exception.

```python
def parse_required_int(raw_value: str) -> int:
    try:
        return int(raw_value)
    except ValueError as error:
        raise ValueError(f"invalid integer: {raw_value!r}") from error
```

Situation : la conversion est obligatoire.

Décision : `raise`.

Situation : la conversion est optionnelle.

Décision : `return None`.

Situation : une exception précise existe.

Décision : attraper l'exception précise, pas `Exception`.

---

## 4. Erreur qui remonte

Situation : la fonction basse ne sait pas quoi faire de l'erreur.

Décision : ne pas l'attraper.

```python
def read_file(path: Path) -> str:
    return path.read_text(encoding="utf-8")
```

Situation : le fichier existe.

Décision : retourner le contenu.

Situation : le fichier manque.

Décision : laisser `FileNotFoundError` remonter.

Situation : l'erreur est déjà claire.

Décision : ne pas ajouter de `try/except`.

---

## 5. Erreur technique à rendre lisible

Situation : l'erreur Python est trop technique pour ton application.

Décision : transformer en exception applicative.

```python
class AppError(Exception):
    pass


class InputFileError(AppError):
    pass


def read_input_file(path: Path) -> str:
    try:
        return path.read_text(encoding="utf-8")
    except FileNotFoundError as error:
        raise InputFileError(f"input file not found: {path}") from error
```

Situation : l'erreur doit parler métier.

Décision : créer une exception applicative.

Situation : `ValueError` suffit.

Décision : ne pas créer de classe inutile.

---

## 6. Traitement batch

Situation : plusieurs éléments sont indépendants.

Décision : attraper l'erreur par élément.

```python
valid_items = []
error_items = []

for index, item in enumerate(items, start=1):
    try:
        valid_item = validate_item(item)
    except AppError as error:
        error_items.append({"index": index, "error": str(error)})
    else:
        valid_items.append(valid_item)
```

Situation : un élément est invalide.

Décision : l'ajouter au rapport d'erreurs.

Situation : un élément est valide.

Décision : l'ajouter aux résultats valides.

Situation : une erreur globale arrive.

Décision : laisser remonter ou arrêter proprement.

---

## 7. Point d'entrée

Situation : une erreur prévue arrive au niveau final.

Décision : afficher, logger, retourner un exit code.

```python
def main() -> int:
    try:
        run()
    except AppError as error:
        print(f"Error: {error}")
        return 1

    return 0
```

Situation : erreur applicative prévue.

Décision : attraper `AppError`.

Situation : bug inattendu.

Décision : ne pas le cacher avec `except Exception`.

Situation : CLI en échec.

Décision : retourner un code différent de zéro.

---

## 8. Quand créer une classe d'exception

Situation : l'erreur a un sens métier.

Décision : créer une exception personnalisée.

Situation : plusieurs erreurs appartiennent à ton application.

Décision : créer une classe parent `AppError`.

Situation : tu veux attraper les erreurs prévues sans attraper les bugs.

Décision : attraper `AppError`, pas `Exception`.

Situation : l'exception standard est claire.

Décision : garder l'exception standard.

---

## Anti-règles

Ne pas faire `except: pass`.

Ne pas utiliser `except Exception` par réflexe.

Ne pas retourner `0`, `""`, `[]` ou `False` pour cacher une erreur.

Ne pas faire `print()` dans une fonction basse.

Ne pas attraper une erreur si tu ne sais pas quoi faire.

Ne pas transformer une erreur en donnée valide.

---

## Phrase finale

`None` = absence normale.

`raise` = contrat impossible.

Propagation = laisser remonter jusqu'au bon niveau.

Catch final = transformer l'erreur en message, log, rapport ou exit code.
