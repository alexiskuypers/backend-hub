# Pull request

## Objectif

Une pull request permet de proposer les changements d’une branche pour qu’ils soient relus avant d’être intégrés dans une autre branche, souvent `main`.

Elle sert à présenter clairement une modification : ce qui a été changé, pourquoi, comment le tester, et s’il y a des points à vérifier.

## Pourquoi c’est important

C’est important parce que dans un vrai projet, on ne modifie pas directement `main` sans contrôle.

Une pull request permet de :

* relire le code avant le merge ;
* expliquer l’objectif de la modification ;
* vérifier les changements fichier par fichier ;
* discuter d’un problème ou d’un choix technique ;
* lancer des tests automatiques ;
* garder une trace claire de l’évolution du projet ;
* éviter de casser la branche principale.

Dans un projet backend, cela aide à vérifier qu’une nouvelle fonctionnalité, une correction de bug ou une modification de configuration est claire, testée et compréhensible.

## Points clés

* Une pull request se fait généralement depuis une branche de travail vers `main`.
* La branche doit contenir des commits propres et cohérents.
* Le titre doit expliquer clairement la modification.
* La description doit expliquer le contexte, les changements et comment tester.
* Une pull request peut être relue avant d’être mergée.
* Elle peut contenir des commentaires, demandes de correction et discussions.
* Le merge final intègre la branche dans la branche cible.
* Une pull request est surtout utilisée sur une plateforme comme GitHub.

## Commandes / exemples

Créer une branche de travail :

```bash
git switch -c add-logging
```

Faire les modifications, puis vérifier :

```bash
git status
git diff
```

Préparer et committer :

```bash
git add src/
git commit -m "add execution logging"
```

Pousser la branche sur GitHub :

```bash
git push -u origin add-logging
```

Ensuite, sur GitHub :

```text
Open pull request
base: main
compare: add-logging
```

Exemple de titre de pull request :

```text
Add execution logging
```

Exemple de description :

````md
## Objectif

Ajouter des logs d’exécution pour mieux diagnostiquer le fonctionnement de l’outil CLI.

## Changements

- Ajout d’une configuration de logging.
- Ajout de logs au démarrage et à la fin du traitement.
- Ajout de logs en cas d’erreur.

## Comment tester

```bash
python -m mini_file_audit.cli example/ --output output/report.csv
````

## Points à vérifier

* Les logs sont lisibles.
* Aucun fichier généré inutile n’est commité.

````

## Ce que ça veut dire

Une pull request est une proposition de changement.

Elle ne sert pas seulement à fusionner une branche. Elle sert surtout à rendre la modification lisible pour quelqu’un d’autre.

Même si je travaille seul, faire une pull request peut m’aider à vérifier mon propre travail avant de merger dans `main`.

## Erreurs à éviter

- Créer une pull request trop grosse avec plusieurs sujets mélangés.
- Mettre un titre vague comme `update`, `fix` ou `changes`.
- Ne pas expliquer pourquoi la modification existe.
- Ne pas indiquer comment tester.
- Ouvrir une pull request avec des fichiers inutiles : `.venv`, logs, caches, fichiers générés.
- Oublier de vérifier `git status` avant de push.
- Faire une pull request alors que les commits sont confus ou non liés.
- Merger sans relire les fichiers modifiés.

## Utilisé dans

- Projet : surtout utile dans les projets hébergés sur GitHub ou en collaboration.
- Situation concrète : proposer une modification depuis une branche de travail vers `main`.
- Exemple backend : ajouter une option CLI, pousser la branche sur GitHub, ouvrir une pull request, relire les changements, puis merger.

Exemple :

```bash
git switch -c add-output-option
# modifications
git add src/cli.py README.md
git commit -m "add output option to CLI"
git push -u origin add-output-option
````

Puis ouverture de la pull request sur GitHub.

## Questions à savoir répondre

1. À quoi sert une pull request ?
2. Quelle est la différence entre une branche et une pull request ?
3. Pourquoi faut-il éviter de travailler directement sur `main` ?
4. Que doit contenir une bonne description de pull request ?
5. Pourquoi une pull request trop grosse est difficile à relire ?
6. Quelle commande permet de pousser une branche locale vers GitHub ?
7. Que veut dire `base: main` et `compare: ma-branche` ?
8. Pourquoi faire une pull request peut être utile même quand je travaille seul ?

## Résumé personnel

Une pull request est une proposition de modification.
Elle permet de présenter le travail fait sur une branche, de le faire relire, de le tester et de l’intégrer proprement dans `main`.


branche locale → push branche → PR GitHub → merge GitHub → pull local
