# Sélection de commits dans git

Il existe plusieurs moyens pour sélectionner des commits dans git :

- le sha1 de 40 caractères
- la sélection par les 4 premiers caractères (au minimum peut être plus) du sha1 (si il n'y a pas d'autres commits avec les mêmes 4 premiers caractères). 
- la sélection par le nom de la branche, dans le cas ou l'on met le nom de la branche à la place du sha1 alors on aura accès au dernier commit de cette branche. 
- Par l'utilisation du reflog, la commande `git reflog` permet d'accéder au reflog qui lui-même va indexer l'état de vos branches à un moment donné dans le temps. 
  - Vous pourrez ainsi utilisaer la syntaxe git show master@{yesterday} pour savoir l'état de votre master hier. 
  - Attention cependant le reflog est strictement local, et ne fonctionne que pour vos références locales. 
- Références d'ancêtres : en ajoutant un `^` à la fin d'une référence de commit vous pourrez voir son ancêtre, cad le commit précédent. Si l'on rajoute un numéro de cette façon `^2` on pourra voir les 2 parents (cas d'un merge), si l'on rajoute le tilde et un chiffre le nombre d'ancêtres constitués par le tilde. 

On peut également sélectionner des commits par "range" :

- la syntaxe en double points : elle permet de sélectionner une range de commits qui sont atteignables depuis une branche mais pas depuis un autre. 

> Considérons l'image suivante : 
>
> ![image](https://git-scm.com/book/en/v2/images/double-dot.png) 
>
> Si on utilise la syntaxe `git log master..experiment` on obtiendra D C comme retour, a savoir les logs sont non accessibles par master mais accessibles par experiment. 
>
> Cela vous permet de mapper vos commits et de savoir ce qui a été mergé ou non de manière plus facile.

- Des syntaxes tripartites existent également : `git log refA refB ^refC` va considérer tous les commits accessibles par refA ou refB mais pas par refC (une autre syntaxe est possible pour ce cas : `git log refA refB --not refC`)

- La syntaxe en `...` donne tous les commits accessibles par l'une ou l'autre des références mais non accessibles aux deux simultanément. On peut rajouter également `--left-right` pour rendre plus explicite le retour, cela permettra de savoir de quel cote est accessible le commit. Exemple 1 : `git log master...experiment` Exemple 2 : `git log --left-right master...experiment`

# Staging interactif

Le staging interactif va vous permettre de rentrer dans un mode interactif et donc d'affiner ce que vous allez passer en stage

Pour renter en mode interactif il vous faudra utiliser la commande suivante : `git add -i` ou `git add --interactive` 
>$ git add -i
>           staged     unstaged path
>  1:    unchanged        +0/-1 TODO
>  2:    unchanged        +1/-1 index.html
>  3:    unchanged        +5/-1 lib/simplegit.rb
>
>*** Commands ***
>  1: [s]tatus     2: [u]pdate      3: [r]evert     4: [a]dd untracked
>  5: [p]atch      6: [d]iff        7: [q]uit       8: [h]elp
>What now>

L'image montre un staging interactif, vous pourrez choisir un certain nombre de commandes que nous allons détailler maintenant. 

## Update 

En tappant u ou 2 au prompt vous pourrez updater le statut, il vous suffira de sélectionner les fichiers à stager (avec une étoile). 

## Revert

Fonction inverse de l'update permet de sortir des fichiers stagés de la staging area (`r` ou 3)

## Diff

Vous permet de sélectionner les fichiers stagés, et de voir les diffs à l'intérieur de ces fichiers (`d` ou 4)

## Staging partiel de fichiers

Vous permet de ne passer que certaines parties du fichier en staging area, si vous avez effectuer deux modifications du même fichier vous pouvez en sélectionner que l'une des deux à stager (`p` ou 5)


# Stashing

Le stashing permet de ne pas commit un état non finalisé de votre working repository. L'exemple typique est que vous devez changer de branche pour résoudre un bug, dans ce cas vous allez donc stasher vos modifications plutôt que les commits. 

Le git stash va s'utiliser via la commande suivante : `git stash`. Il va concrètement stocker l'état de votre working directory et ensuite le faire revenir à l'état de la création initiale de la branche. Ainsi vous pouvez changer de branche sans craindre de pertes de données. 

Lorsque vous voudrez retrouver l'état de votre working directory avant le stash vous utiliserez la commande : `"git stash list`. Cette dernière va vous permettre de localiser les stashs sauvegardés. Pour revenir à l'état d'avant stash il ne vous restera qu'à appliquer la commande `git stash apply` pour le dernier stash ou `git stash apply <NOM DU STASH>` pour un stash plus ancien. 

Si vous aviez des fichiers stagés au moment du commit vous pouvez ajouter l'option `--index` qui reprendra l'état d'indexation précédent le stash. Une option permet de conserver l'index au niveau du stash il faut alors effectuer `git stash --keep-index`.

Le stash ne va prendre en compte que les fichiers trackés si on ne précise pas un comportement différent. L'ajout de l'option `-u` va permettre de prendre en compte les fichiers non trackés. L'ajout de l'option `--all` prendra non seulement l'état des fichiers non trackés mais aussi celui des fichiers explicitement exclus par le gitignore. 

Enfin l'option `--patch` vous permet de sélectionner interactivement ce que vous voulez stasher ou non. 

Vous avez également la possibilité de créer une nouvelle branche à partir du stash avec la commande suivante `git stash branch <NOM BRANCHE A CREER>`

# Git clean

Bien que git clean ait des aspects similaires au stash, il permet quant à lui de se défaire totalement des modifications et non pas de les réutiliser pour une utilisation future. 

Attention cette commande va supprimer du contenu de fichiers non trackés et ne sera pas reversible on préférera généralement un `git stash --all` cette dernière n'etant pas destructrice contrairement à `git clean`.

Vous pouvez ajouter l'option `-x` qui va supprimer tous les fichiers trackés ou non.

Avant de vous lancer dans une opération trop destructrice deux options s'offrent à vous : ajouter l'option `-n` qui va vous indiquer ce qui sera supprimé par la comande sans pour autant le supprimer ou jouer la commande en mode interactif en ajoutant le `-i`.

Pour forcer l'exécution de la commande il faudra rajouter l'option `-f`

# Git grep

Outil de recherche par excellence, git fournit un grep proche des greps que vous pouvez déjà connaître dans les systèmes unix. Il permettra notamment avec l'option -n de connaître les numéros de ligne ou se trouve l'occurrence que vous recherchez. On ne rentrera pas dans le détail dans cet outil dans le cadre de la formation, son fonctionnement devant vous être famillier.

# Recherche dans les logs 

L'option `-S` de la commande `git log` vous permet de chercher à l'intérieur des logs une expression afin de localiser le moment ou une expression est apparue dans les logs. Il est également possible de fournir une expression régulière avec l'option `-G` 

L'option `-L` permet d'étudier l'évolution d'une fonction ou d'une ligne de code dans la database de git. 

# Travail de l'historique des commits 

Il est possible de réviser l'historique des commits notamment en faisant les actions suivantes : 

- Changer l'ordre des commits
- Changer les messages de commit
- Modifier les fichiers présents dans un commit
- Regrouper ou splitter des commits
- Supprimer des commits

Ceci est possible avant que vous partagiez votre travail avec les autres. 

## Modifications dans le dernier commit 

Nous avons déjà vu que pour modifier le dernier commit il suffit de restager les modifications puis d'utiliser la commande `git commit --amend`, il en va de même pour modifier le message du dernier commit. 

Attention amender le commit modifie le SHA1 du commit, si vous avez déjà poussé le commit n'utilisez pas cette commande. 

## Changements sur plusieurs commits 

Pour cela nous utiliserons la commande rebase avec l'option `-i` pour interactif tout en précisant le nombre de commit jusqu'auquel nous voulons remonter, en ajoutant `HEAD~X` ou X est le nombre de commits auxquels nous voulons accéder -1, puisque le dernier commit est déjà compris dans le head simple. 

Cette commande va ouvrir un éditeur de texte avec la liste de vos commits, pour chaque commit que vous souhaitez retravailler il vous suffira de modifier `pick` par `edit`.

Pour chaque commit à éditer le script s'arrêtera et vous demandera de faire les modifications nécessaires puis faire un `git commit --amend` puis un `git rebase continue`.

Attention a ne pas utiliser cette commande si vous avez déjà poussé les commits, cela serait perturbant pour vos collègues. 

## Fusionner des commits

L'outil de rebase interactif vous laisse également fusionner des commits. Vous lancerez l'outil de la manière ou nous l'avons vu précédemment puis vous remplacerez `edit` par `squash`, ce qui aura pour effet de fusionner tous les commits ensemble, les messages de chacun des commits seront alors également fusionnés.

## Splitter un commit

On utilisera toujorus la commande `git rebase -i` puis on passera en `edit` le commit que nous souhaitons splitter. Une fois arrivé à la ligne de commande du commit à splitter nous utiliserons `git reset` pour défaire le commit, puis nous restagerons et recommiterons les fichiers jusqu'à satisfaction, avant de réutiliser `git rebase --continue`.

## Supprimer un commit

Pour cela il faut également utiliser la commande `git rebase -i` puis ensuite remplacer `pick` par `drop`.

Attention cependant la suppression d'un commit entrainera la recréation de tous les commits survenus après ce commit supprimé, ce qui aura pour impact de créer potentiellement beaucoup de conflits de merge. 

Il est possible de retourner à l'état initial du dépôt en entrant la commande `git rebase --abort`, il est également possible d'utiliser reflog si vous souhaitez revenir à un état antérieur du dépôt après avoir finalisé votre commande. 

# Filter-branch

Cette option permet de très larges réécriture de votre histoire. Cependant attention à ne pas l'utiliser si vous avez rendu vos changements publiques cela pourrait créer des conflits importants, néanmoins lorsque vous préparez la publication d'un repository cet outil peut être très puissant. 

## Supprimer un fichier de tous les commits

Il est possible de supprimer un fichier de tous les commits avec la commande suivante : 

> `git filter-branch --tree-filter 'rm -f <NOM DU FICHIER>' HEAD`

L'option tree filter va supprimer chaque occurrence du fichier puis réeffectuer les commits nécessaires à sa suppression. 

Une bonne option consiste généralement à faire ce genre de changements dans une nouvelle branche puis ensuite à merger cette branche avec le master. 

## Modifier le sous répertoire racine

La commande `git filter-branch --subdirectory-filter <NOM DU SOUS REPERTOIRE> HEAD` vous permet de recréer tout le projet dans un sous-répertoire donné, il sera donc la racine de tous vos fichiers. 

# Git Reset
