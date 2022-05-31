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

![image](https://git-scm.com/images/bg/body.jpg)

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

Attention cette commande va supprimer du contenu de fichiers non trackés et ne sera pas reversible on préférera généralement un `git stash --all` cette dernière n'etant pas destructrive contrairement à `git clean`.

