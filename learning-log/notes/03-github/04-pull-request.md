# Pull requests

## Objectif

Une pull request permet de montrer une évolution de code claire avant de l’intégrer dans une branche principale, souvent `main`.

Elle sert à présenter le travail fait sur une branche : les fichiers modifiés, les commits, l’objectif de la modification et la manière de la tester.

## Pourquoi c’est important

Une pull request permet à une autre personne de comprendre rapidement ce qui a changé dans le projet.

Dans un projet backend Python, elle aide à vérifier :

* que la modification a un objectif clair ;
* que les fichiers modifiés sont cohérents ;
* que le code peut être relu facilement ;
* que les tests passent ;
* que le README ou la documentation sont mis à jour si nécessaire ;
* que la modification peut être intégrée dans `main` sans casser le projet.

Une bonne pull request ne sert pas seulement à merger du code.
Elle sert à rendre le changement compréhensible.

## Points clés

* Une pull request part généralement d’une branche de travail vers `main`.
* Elle doit contenir une modification logique, pas plusieurs sujets mélangés.
* Le titre doit être clair.
* La description doit expliquer le contexte, les changements et la méthode de test.
* Les commits doivent être compréhensibles.
* Le diff doit être relu avant le merge.
* Une pull request peut être liée à une issue.
* Une pull request trop grosse devient difficile à relire.
* Le merge intègre les changements dans la branche cible.

## Commandes / exemples

Créer une branche de travail :

```bash
git switch -c add-recursive-option
```

Faire les modifications, puis vérifier :

```bash
git status
git diff
```

Préparer et committer :

```bash
git add .
git commit -m "add recursive scan option"
```

Pousser la branche sur GitHub :

```bash
git push -u origin add-recursive-option
```

Sur GitHub, créer une pull request :

```text
base: main
compare: add-recursive-option
```

Cela veut dire :

```text
Je propose d’intégrer les changements de add-recursive-option dans main.
```

## Exemple de pull request claire

Titre :

```text
Add recursive scan option
```

Description :

````md
## Objectif

Ajouter une option `--recursive` pour permettre à la CLI de scanner aussi les sous-dossiers.

## Changements

- Ajout de l’option `--recursive`.
- Adaptation de la fonction de scan.
- Ajout d’un test pour le scan récursif.
- Mise à jour du README.

## Comment tester

```bash
pytest
mini-file-audit examples/sample-folder --recursive
````

## Issue liée

Closes #3

````

## Ce que ça veut dire

Une pull request est une proposition de changement.

Elle permet de comparer deux branches :

- `base` : la branche qui va recevoir les changements ;
- `compare` : la branche qui contient les changements proposés.

Exemple :

```text
base: main
compare: add-recursive-option
````

Cela veut dire que les changements de `add-recursive-option` sont proposés pour être intégrés dans `main`.

## Erreurs à éviter

* Créer une pull request trop grosse.
* Mélanger plusieurs sujets dans une seule pull request.
* Mettre un titre vague comme `update`, `fix` ou `changes`.
* Ne pas expliquer pourquoi la modification existe.
* Ne pas indiquer comment tester.
* Oublier de relire le diff avant de merger.
* Ajouter des fichiers inutiles ou générés.
* Merger une pull request sans vérifier que le projet fonctionne.
* Créer une branche, merger localement, puis push seulement `main` si l’objectif est de faire une vraie pull request.

## Utilisé dans

* Projet : projets GitHub, GitLab ou Bitbucket.
* Situation concrète : proposer une modification lisible avant de l’intégrer dans `main`.
* Exemple backend : ajouter une option CLI, corriger un bug, ajouter des tests, modifier une configuration ou améliorer le README.

Exemple de workflow propre :

```bash
git switch main
git pull
git switch -c fix-invalid-extension-error

# modifications

git status
git diff
git add .
git commit -m "fix invalid extension error"
git push -u origin fix-invalid-extension-error
```

Ensuite, création de la pull request sur GitHub.

## Questions à savoir répondre

1. À quoi sert une pull request ?
2. Quelle est la différence entre une branche et une pull request ?
3. Que signifie `base: main` ?
4. Que signifie `compare: ma-branche` ?
5. Pourquoi une pull request doit-elle être lisible ?
6. Que doit contenir une bonne description de pull request ?
7. Pourquoi faut-il éviter les pull requests trop grosses ?
8. Pourquoi relire le diff avant de merger ?
9. Quelle commande permet de pousser une branche sur GitHub ?
10. Quelle différence entre merger localement puis push, et créer une pull request ?

## Résumé personnel

Une pull request sert à présenter une évolution de code de manière claire.
Elle montre les changements d’une branche, explique pourquoi ils existent, comment les tester, et permet de les intégrer proprement dans `main`.
