# Introduction à la notion de branches

Pour comprendre la notion de branches il faut voir un projet composé d'une ligne directrice et de multiples divergences possibles. 

Prenons un exemple comcret : vous produisez un content management system (CMS). Ce système global est décomposé entre des éléments faisant déjà parti du "canon" de ce CMS : par exemple le système de gestion des articles, celui des utilisateurs etc. Imaginons que vous vouliez maintenant intégrer dans ce système complexe un système de gestion des images. Vous allez avoir besoin de ce "canon" ou en tout cas de l'intégralité du code déjà présent et validé par tous comme point de départ. Néanmoins vous allez créer une divergence, à savoir l'intégration dans ce CMS d'un système de gestion d'images. 

La création d'une branche va vous permettre de créer une copie spécifique, à jour avec la copie canonique vous laissant explorer toutes les modifications nécessaires sans pour autant devoir pousser vers la copie canonique ces modifications.

Une fois que vous êtes satisfait de votre module d'image vous pourrez réunir votre branche gestion images et la branche principale. On appelle cette action "merger" des branches. 

# Conception de git et impact sur les branches dans git

La conception même de git[^1] permet une gestion quasi instantanée des branches. Pour cette raison git encourage l'utilisation de multiples branches et parfois même la création et le merge de plusieurs branches par jour !

Nous avons également vu dans la partie de la conception de git que git fait des pointages vers des états (ou instantanés du code). La raison de la rapidité des branches est qu'une branche est en fait un pointeur spécifique vers un instantané du code (un commit particulier). 

Ainsi le schéma suivant explique ce qui se passe lorsque nous créons une branche "testing" différente de notre master : 

![image](https://git-scm.com/book/en/v2/images/two-branches.png)

*Source : https://git-scm.com/book/en/v2/images/two-branches.png*

Cette nouvelle branche pointe donc vers le commit précédent la divergence (f30ab) , les commits suivants seront associés à cette branche alors que le pointeur de la master restera sur le commit f30ab jusqu'au merge, comme dans l'illustration suivante : 

![image](https://git-scm.com/book/en/v2/images/advance-testing.png)

*Source : https://git-scm.com/book/en/v2/images/advance-testing.png*

# Commande de base sur les branches

## Création d'une nouvelle branche 

La commande `git branch <SHORTNAME >` permet la création d'une nouvelle branche dans le projet. Ainsi si nous voulons créer une nouvelle branche dans le projet git que nous avons pris en exemple, nous pouvons tapper `git branch nouvellebranche`.

Attention la commange `git branch` ne vous fait pas vous déplacer dans la nouvelle branche, elle la crée simplement. Pour que git se souvienne de la branche sur laquelle vous êtes actuellement il crée un nouveau pointeur appelé "head". Cette notion de head permet simplement de savoir sur quelle branche vous vous situez. 

La commande `git log --oneline --decorate` vous permettra de voir ou se situe les pointeurs des différentes branches dont le head. 

## Changement de branche

Puisque la création d'une branche n'engage pas le changement automatiquement, il vous faut donc une commande qui permette de changer de branche, et ce à tout moment. Cette commande est la commande `git checkout <SHORTNAME>`. 

Si l'on reprend l'exemple de la nouvelle branche la commande `git checkout nouvellebranche` vous fera aller directement sur cette branche. Inversement si l'on se situe sur la branche nouvellebranche et que nous voulons retourner sur la branche master : `git checkout master`.

> Il est à noter qu'un changement de branche modifie les fichiers dans votre working directory qui reprendront alors les modifications et l'état de l'une ou l'autre branche !

Vous trouverez une illustration de ce changement ci-après : 

![image](https://git-scm.com/book/en/v2/images/advance-master.png)

*Source : https://git-scm.com/book/en/v2/images/advance-master.png*

[^1]: Se reporter au chapitre 1 partie 4
