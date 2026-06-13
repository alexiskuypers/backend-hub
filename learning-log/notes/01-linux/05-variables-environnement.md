# Variables d’environnement

## Objectif

Les variables d’environnement permettent de configurer un programme depuis l’extérieur du code.

Elles servent à donner des informations à un programme sans écrire directement ces valeurs dans les fichiers du projet.

## Pourquoi c’est important

Dans un projet backend, on utilise souvent des variables d’environnement pour gérer la configuration selon le contexte :

* environnement de travail : développement, test, production ;
* URL de base de données ;
* port de l’application ;
* clés API ;
* secrets ;
* chemins de fichiers ;
* options de debug.

L’idée importante :

> Le code reste le même, mais la configuration peut changer selon l’environnement.

Exemple : en développement, l’application utilise une base locale. En production, elle utilise une vraie base distante. Le code ne doit pas être modifié à chaque fois.

## Points clés

* Une variable d’environnement est une valeur disponible dans le terminal et pour les programmes lancés depuis ce terminal.
* `export` permet de définir une variable accessible aux programmes lancés ensuite.
* `echo $NOM_VARIABLE` permet d’afficher la valeur d’une variable.
* `env` ou `printenv` permettent de voir les variables d’environnement.
* `unset` permet de supprimer une variable dans la session courante.
* Les variables d’environnement sont très utilisées pour éviter d’écrire des secrets directement dans le code.
* Une variable définie dans un terminal n’est pas forcément disponible partout ni pour toujours.

## Commandes / exemples

Définir une variable d’environnement :

```bash
export APP_ENV=dev
```

Lire une variable :

```bash
echo $APP_ENV
```

Afficher toutes les variables d’environnement :

```bash
env
```

Afficher une variable précise :

```bash
printenv APP_ENV
```

Supprimer une variable de la session courante :

```bash
unset APP_ENV
```

Exemple avec une URL de base de données :

```bash
export DATABASE_URL="postgresql://user:password@localhost:5432/mydb"
echo $DATABASE_URL
```

Exemple avec Python :

```bash
export APP_ENV=dev
python main.py
```

## Ce que ça veut dire

Une variable d’environnement permet de passer une information au programme sans la coder directement dans le fichier Python.

Au lieu d’écrire une valeur fixe dans le code, le programme peut lire une valeur fournie par l’environnement.

Exemple mauvais réflexe :

```python
DATABASE_URL = "postgresql://user:password@localhost:5432/mydb"
```

Meilleure logique :

```bash
export DATABASE_URL="postgresql://user:password@localhost:5432/mydb"
```

Puis le programme lit cette variable au moment de son exécution.

## Erreurs à éviter

* Mettre un vrai mot de passe, token ou secret directement dans le code.
* Mettre un fichier contenant des secrets sur GitHub.
* Croire qu’une variable définie dans un terminal existe automatiquement partout.
* Oublier de vérifier la variable utilisée avec `echo $NOM_VARIABLE`.
* Confondre une variable Python avec une variable d’environnement.
* Écrire des valeurs de production dans un projet local ou public.

## Utilisé dans

* Projet : surtout utile dans les projets backend, CLI, Docker, API et applications déployées.
* Situation concrète : configurer une application sans modifier le code.
* Exemple backend : définir l’URL de la base PostgreSQL, le mode `dev` ou `prod`, ou une clé API.
* Exemple projet : dans `ops-file-audit`, on pourrait utiliser une variable d’environnement pour définir le mode d’exécution ou le dossier de sortie par défaut.

## Questions à savoir répondre

1. À quoi sert une variable d’environnement ?
2. Quelle est la différence entre une variable Python et une variable d’environnement ?
3. À quoi sert `export APP_ENV=dev` ?
4. Comment afficher la valeur d’une variable d’environnement ?
5. Pourquoi ne faut-il pas écrire un secret directement dans le code ?
6. Pourquoi une application backend utilise souvent des variables comme `DATABASE_URL`, `APP_ENV` ou `SECRET_KEY` ?
7. Que fait `unset APP_ENV` ?

## Résumé personnel

Une variable d’environnement sert à configurer un programme depuis l’extérieur du code.
C’est essentiel en backend parce que le même code doit pouvoir fonctionner en développement, en test ou en production avec des configurations différentes.
