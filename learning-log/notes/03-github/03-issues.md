# Issues

## Objectif

Une issue sert à découper le travail en tâches concrètes.

Elle permet de décrire clairement ce qu’il faut faire, pourquoi il faut le faire, et quand la tâche peut être considérée comme terminée.

Une issue peut représenter :

* une fonctionnalité à ajouter ;
* un bug à corriger ;
* une amélioration ;
* une tâche de documentation ;
* une tâche de nettoyage ;
* une question technique à résoudre.

## Pourquoi c’est important

Les issues permettent d’éviter de travailler de manière floue.

Dans un projet backend Python, elles aident à :

* organiser le travail ;
* découper un projet en petites étapes ;
* prioriser les tâches ;
* garder une trace de ce qui reste à faire ;
* relier une branche ou une pull request à une tâche précise ;
* éviter les grosses modifications mal contrôlées.

Une bonne issue transforme une idée vague en action claire.

## Points clés

* Une issue doit avoir un titre clair.
* Une issue doit décrire un seul sujet principal.
* Une issue doit expliquer le contexte.
* Une issue doit contenir des tâches concrètes.
* Une issue peut avoir une checklist.
* Une issue peut être liée à une branche ou une pull request.
* Une issue doit avoir une condition de fin claire.
* Une issue trop grande doit être découpée en plusieurs issues plus petites.

## Exemple de mauvaise issue

```text id="tntpjd"
Améliorer le projet
```

Cette issue est trop vague.
On ne sait pas quoi faire, par où commencer, ni quand c’est terminé.

## Exemple de bonne issue

```md id="nut3hc"
# Ajouter une option --recursive à la CLI

## Contexte

Actuellement, la CLI analyse seulement le dossier donné directement.
Je veux pouvoir analyser aussi les sous-dossiers.

## Tâches

- Ajouter une option `--recursive` dans argparse.
- Adapter la fonction de scan.
- Ajouter un test pour le mode récursif.
- Mettre à jour le README.

## Critères de validation

- La commande fonctionne sans `--recursive`.
- La commande fonctionne avec `--recursive`.
- Les tests passent avec `pytest`.
- Le README contient un exemple d’utilisation.
```

## Commandes / exemples

Créer une branche liée à une issue :

```bash id="qjydmx"
git switch -c add-recursive-option
```

Faire les modifications :

```bash id="hj3u9w"
git status
git diff
```

Commiter la tâche :

```bash
git add .
git commit -m "add recursive scan option"
```

Pousser la branche :

```bash id="t0mlv8"
git push -u origin add-recursive-option
```

Dans une pull request, on peut mentionner l’issue :

```
Closes #3
```

Cela veut dire que la pull request fermera l’issue numéro 3 quand elle sera mergée.

## Ce que ça veut dire

Une issue n’est pas seulement une note ou une idée.

C’est une tâche de travail structurée.

Elle doit permettre de répondre rapidement à trois questions :

* Qu’est-ce qu’il faut faire ?
* Pourquoi faut-il le faire ?
* Comment savoir que c’est terminé ?

## Erreurs à éviter

* Créer des issues trop vagues.
* Mettre plusieurs sujets différents dans une seule issue.
* Ne pas définir de critères de validation.
* Ne pas découper une grosse tâche.
* Créer une issue impossible à terminer clairement.
* Oublier de fermer l’issue quand la tâche est terminée.
* Utiliser les issues comme simple brouillon sans action concrète.
* Faire une branche ou une pull request sans lien clair avec une tâche.

## Utilisé dans

* Projet : projets GitHub, surtout quand le travail doit être organisé.
* Situation concrète : découper un projet en petites tâches avant de coder.
* Exemple backend : créer une issue pour ajouter une option CLI, corriger un bug de parsing, ajouter des tests ou améliorer le README.

Exemple de découpage pour une CLI Python :

```text id="7m14hx"
Issue 1 : créer la structure du projet
Issue 2 : ajouter la lecture des arguments CLI
Issue 3 : scanner les fichiers d’un dossier
Issue 4 : générer un rapport CSV
Issue 5 : ajouter les tests
Issue 6 : améliorer le README
```

## Questions à savoir répondre

1. À quoi sert une issue ?
2. Quelle est la différence entre une idée vague et une issue claire ?
3. Que doit contenir une bonne issue ?
4. Pourquoi faut-il éviter les issues trop grosses ?
5. À quoi servent les critères de validation ?
6. Quelle différence entre une issue, une branche et une pull request ?
7. Que veut dire `Closes #3` dans une pull request ?
8. Pourquoi les issues sont utiles même quand je travaille seul ?

## Résumé personnel

Une issue sert à transformer une idée ou un problème en tâche concrète.
Elle doit expliquer quoi faire, pourquoi le faire, et comment vérifier que c’est terminé.
