# Permissions Linux

## Objectif

Les permissions Linux permettent de contrôler qui peut lire, modifier ou exécuter un fichier ou un dossier.

Elles distinguent trois catégories :

* `user` : le propriétaire du fichier ;
* `group` : le groupe associé au fichier ;
* `others` : les autres utilisateurs.

Elles distinguent aussi trois droits :

* `r` = read = lire ;
* `w` = write = écrire / modifier ;
* `x` = execute = exécuter ou traverser.

## Pourquoi c’est important

Ce concept est important car il permet de sécuriser les fichiers d’un projet et d’éviter que n’importe quel utilisateur puisse lire, modifier, supprimer ou exécuter des éléments sans autorisation.

Dans un projet backend, les permissions peuvent servir à :

* rendre un script exécutable ;
* éviter de donner trop de droits à des fichiers sensibles ;
* comprendre une erreur `Permission denied` ;
* protéger des fichiers de configuration ou des secrets.

## Points clés

* Les permissions sont séparées entre `user`, `group` et `others`.
* Les droits principaux sont `read`, `write` et `execute`.
* Le mode numérique utilise :

  * `4` = lecture ;
  * `2` = écriture ;
  * `1` = exécution.
* Le mode symbolique utilise :

  * `u` = user ;
  * `g` = group ;
  * `o` = others ;
  * `a` = all.
* `chmod` modifie les permissions.
* `ls -l` permet de voir les permissions.
* `chmod 777` donne tous les droits à tout le monde et doit être évité.

## Commandes / exemples

Voir les permissions :

```bash
ls -l
```

Ajouter le droit d’exécution au propriétaire :

```bash
chmod u+x script.py
```

Donner lecture, écriture et exécution au propriétaire, lecture et exécution aux autres :

```bash
chmod 755 script.py
```

Donner lecture/écriture au propriétaire, lecture seule au groupe et aux autres :

```bash
chmod 644 fichier.txt
```

Définir précisément les droits :

```bash
chmod u=rwx,go=r fichier.txt
```

Retirer le droit d’écriture au groupe :

```bash
chmod g-w fichier.txt
```

Commande dangereuse à éviter par facilité :

```bash
chmod 777 fichier.txt
```

## Ce que ça veut dire

Linux applique les permissions séparément au propriétaire, au groupe et aux autres utilisateurs.

Exemple :

```bash
-rwxr-xr--
```

Cela veut dire :

* `-` : fichier normal ;
* `rwx` : le propriétaire peut lire, modifier et exécuter ;
* `r-x` : le groupe peut lire et exécuter ;
* `r--` : les autres peuvent seulement lire.

Pour un fichier, `x` signifie qu’il peut être exécuté comme programme ou script.

Pour un dossier, `x` signifie qu’on peut entrer ou traverser ce dossier.

## Erreurs à éviter

* Donner tous les droits à tout le monde avec `chmod 777` par facilité.
* Modifier des permissions sans comprendre l’effet.
* Oublier que `x` n’a pas exactement le même rôle sur un fichier et sur un dossier.
* Ne pas vérifier les permissions avec `ls -l` quand j’ai une erreur `Permission denied`.
* Donner trop de droits à des fichiers sensibles comme `.env`.

## Utilisé dans

* Projet : tous les projets.
* Situation concrète : rendre un script exécutable ou comprendre pourquoi un fichier ne peut pas être lu/modifié/exécuté.
* Exemple backend : rendre un script de lancement exécutable avec `chmod u+x run.sh`, ou vérifier qu’un fichier sensible n’est pas accessible à tout le monde.

## Questions à savoir répondre

1. Quelle est la différence entre `user`, `group` et `others` ?
2. Que signifient `r`, `w` et `x` ?
3. Quelle est la différence entre `chmod 755` et `chmod 777` ?
4. Pourquoi `chmod 777` est une mauvaise habitude ?
5. Que vérifier si le terminal affiche `Permission denied` ?
6. Que signifie une permission comme `-rwxr-xr--` ?
