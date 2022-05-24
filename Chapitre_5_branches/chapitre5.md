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

# Commandes de base sur le branching et le merging

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

## Merging et cas d'utilisation avancée

Si jusqu'ici nous avons vu un cas simple : vous travaillez sur une nouvelle feature (la gestion d'image de votre CMS), voyons maintenant un cas plus avancé. 

Alors que vous travaillez sur cette feature planifiée, un bug vous est remonté sur le coeur de votre application, disons pour l'exemple il n'est pas possible d'enregistrer un article ayant moins de 100 caractères. Ce bug étant critique pour votre application vous devez absolument travaillé tout de suite dessus !

Etant donné que vous avez créé une nouvelle branche pour votre feature d'image, votre premier reflexe est de revenir à l'état précédant les modifications de cette branche. 

Avant de switcher vers la branche master, une bonne pratique pour limiter le risque est de procéder à un commit de l'état actuel de vos modifications sur la branche images afin de limiter le risque de conflit ou de pertes de données : `git commit -a -m "enregistrement de l'état actuel des modifications"`

Vous exécutez ensuite la commande `git checkout master`. 

Vous travaillez sur votre hotfix puis vous le commitez `git commit -a -m "correction bug article < 100 charactères"` 

Enfin vous pushez ce nouveau hotfix vers le dépôt distant avec la commande `git pull`, votre branche master étant programmée pour le suivi de la branche master distante. 

Puis vous retournez sur votre branche image `git checkout image`. 

Vous retrouvez donc l'état de votre branche avant le hotfix. La problématique étant que cette branche a divergé avant le hotfix, du coup vous êtes sur une branche qui n'intègre pas encore les modifications du hotfix. Si vous la mergez dans la branche principale le bug se reproduira à nouveau !

Il vous faut donc merger votre branche master dans la branche images pour que vous bénéficiez des dernières modifications poussées dans la branche master.

Pour cela il faut se rendre dans la branche à l'intérieure de laquelle vous souhaitez effectuer ce merge. En l'occurrence nous sommes déjà sur la branche images. 

Pour réaliser ce merge nous allons devoir utiliser la commande `git merge master`, ce qui va intégrer les modifications de la branche master dans votre branche locale. 

Vous continuez ensuite le travail, puis vous finissez cette feature d'image. Lorsque vous êtes satisfait de votre travail sur cette branche vous voulez ensuite l'intégrer dans master. Voici donc la suite de commandes que vous allez effectuer : 

`git commit -a -m "Finalisation de la feature image"`

`git checkout master`

`git merge image`

La branche image vous étant désormais inutile vous pouvez maintenant l'effacer avec la commande `git branch -d <SHORTNAME>` soit dans notre cas `git branch -d image`.

## Gestion des conflits autour du merge

Dans notre cas d'exemple nous avons travaillé directement sur la branche master pour la résolution du bug. Dans la pratique nous aurions créé une branche spécifique à la résolution du bug puis nous l'aurions mergé à la branche master. 

Il y a de fortes probabilités que notre branche de résolution de bug et la branche image aient modifié les mêmes parties d'un ou plusieurs fichiers. Lorsque cela se produit, git n'est pas capable de merger automatiquement les branches. 

Etudions donc ce qui se passe dans ce cas. 

>git merge image
>
>Auto-merging index.html
>
>CONFLICT (content): Merge conflict in index.html
>
>Automatic merge failed; fix conflicts and then commit the result.

Si nous étudions ce retour, nous pouvons mieux nous apercevoir de la problématique. Tout d'abord revenons sur ce que fait concrètement un merge dans git. Il va sauvegarder un nouvel instantané avec le "mix" des deux branches et créer ainsi un nouveau commit. 

Dans ce cas précis le processus a été arrếté avant que le commit n'ait lieu car le "mix" des fichiers n'a pas pu se produire étant donné que deux modifications étaient conflictuelles. 

La commande `git status` liste l'ensemble des fichiers qui comportent un conflit et les marque comme non mergés. 

Git va alors marquer automatiquement dans ces fichiers les passages qui sont problématiques. Ouvrons donc le fichier index.html qui nous pose soucis dans cet exemple voici ce que nous trouverions : 

```html
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> image:index.html
```

Si l'on se rappelle de ce que nous avons vu précédemment HEAD fait référence à la branche dans laquelle nous nous situons, à savoir celle dans laquelle nous voulions merger la branche image (donc le master).

La syntaxe permet de savoir le contenu du head. il est contenu entre <<<<<<< HEAD:NOM DU FICHIER et les =======. En dessous de ces signes "égal" se situent les modifications de la branche image. 

Pour résoudre le conflit il faudra alors supprimer tous les éléments jusqu'a conserver la partie de code que nous considérons comme bonne. 

Ainsi le bloc : 

```html
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> image:index.html
```

Devra être remplacé entièrement par : 

```html
<div id="footer">
 please contact us at email.support@github.com
</div>
```

En partant du principe que nous voulons conservé ce qui est dans image. 

Si nous souhaitons conserver ce qui est dans le master on remplacera le bloc par : 

```html
<div id="footer">contact : email.support@github.com</div>
```

[^1]: Se reporter au chapitre 1 partie 4
