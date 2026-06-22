# Encodage

## Rôle du concept

L’encodage définit comment les caractères d’un fichier sont transformés en octets.

L’encodage est la règle utilisée pour convertir :

texte lisible   <====>   octets stockés dans le fichier

Par exemple, les caractères suivants doivent être représentés sous forme d’octets :

A
é
ç
€
李

Python doit savoir quelle règle utiliser pour transformer ces octets en caractères.
Utiliser explicitement UTF-8 permet de lire et écrire correctement les accents, symboles et caractères internationaux.

## Exemples

Lecture d’un fichier en UTF-8 :

```python
content = path.read_text(encoding="utf-8")
```

Avec `open()` :

```python
with path.open("r", encoding="utf-8", newline="") as file:
    content = file.read()
```

Gestion d’une erreur d’encodage :

```python
try:
    content = path.read_text(encoding="utf-8")
except UnicodeDecodeError as error:
    raise FileEncodingError(
        f"Unable to decode file '{path}' as UTF-8"
    ) from error
```

## Erreur typique

Ne pas préciser l’encodage :

```python
content = path.read_text()
```

Le résultat peut dépendre du système d’exploitation.

Autres erreurs fréquentes :

* utiliser le mauvais encodage ;
* ignorer silencieusement les caractères invalides ;
* lire en UTF-8 puis écrire avec un autre encodage ;
* remplacer automatiquement les caractères sans prévenir l’utilisateur.

## Règle à retenir

Toujours préciser explicitement l’encodage :

```python
encoding="utf-8"
```

Si le fichier n’est pas compatible, produire une erreur claire plutôt que de modifier silencieusement les données.

Utiliser `utf-8-sig` seulement lorsqu’il faut accepter un fichier UTF-8 contenant un BOM, fréquent dans certains exports Excel.

## Utilité en projet

Dans `data-contract-cli`, l’encodage doit être utilisé pour :

* lire le CSV d’entrée ;
* lire le contrat YAML ;
* écrire le CSV propre ;
* écrire le rapport d’erreurs ;
* écrire le résumé JSON.

L’encodage peut être défini dans le contrat :

```yaml
encoding: "utf-8"
```

Une erreur d’encodage doit produire un message exploitable et l’exit code prévu pour les erreurs de fichier.
