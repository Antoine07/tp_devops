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

# Commandes de base sur le branching, le merging et leur gestion

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

Il est également à noter que git fournit un outil visuel pour la résolutiond de conflit appelable par la commande `git mergetool`, enfin il est possible de configurer les outils de résolution de conflits visuels. La liste des outils accessibles est disponible lors de l'appel de la commande. 

## Les commandes de gestion des branches

La commande `git branch` va vous permettre de gérer plus largement les branches.

Tout d'abord utilisée sans arguments elle permet de lister les branches disponibles. Lors de ce listing la branche où vous vous situez sera précédée d'un *

La commande `git branch -v` permet de voir le dernier commit sur chaque branche. 

La commande `git branch --merged` liste les branches qui ont été mergées dans la branche actuelle (l'option --no-merged fait l'inverse). Cette commande permet de voir les branches qui sont sujettes à être effacées. Vous pouvez également appliquer cette commande à d'autres branches dans lesquelles vous ne vous situez pas en rajoutant le nom de cette branche `git branch --merged <NOM BRANCHE>`.

L'option `--move` vous permet de renommer une branche localement avec la syntaxe suivante `git branch --move <NOM ACTUEL> <NOUVEAU NOM>`. Cette modification n'est toutefois que local, il faudra la rendre disponible à tous avec la commande suivante : `git push --set-upstream origin <NOUVEAU NOM>`. Il vous restera enfin à effacer l'ancienne branche avec `git push origin --delete <ANCIEN NOM>`.

Il est néanmoins conseiller de ne pas renommer la branche principale d'un projet pour des raisons de sécurité et cohérence.

# Logiques de gestion des branches

Maintenant que nous avons vu les éléments techniques de gestion des branches nous devons comprendre les logiques qui président à la création, le merge, et l'effacement des branches dans une logique projet. 

Il faut tout d'abord introduire une notion, à savoir celle de branches de stabilité progressive. 

Selon ce principe il peut exister plusieurs branches parallèles chacune allant d'un niveau de stabilité élevé à un niveau moins élevé. Ainsi l'organisation basique de ce principe correspond au schéma suivant : 

![image](https://git-scm.com/book/en/v2/images/lr-branches-2.png)

*Source https://git-scm.com/book/en/v2/images/lr-branches-2.png *

Dans cet exemple l'organisation est la suivante : 
  * la branche master est celle qui fait preuve de la plus grande stabilité elle ne contient que des éléments prêts à être déployés ou déjà déployés. Tous les éléments qui sont mergés dans cette branche ont été rigoureusement testés auparavant. 
  * la branche développement comprend des éléments qui peuvent parfois être non stables et le développement de long terme. Elle sert de branche de test avant la validation de ces changements avant le merging vers la branche master. 
  * la branche topic comprend les éléments de développement ponctuels (comme notre hotfix précédemment). Elles sont donc des branches à la durée de vie beaucoup plus courte uniquement destinées à accomplir la fonction pour laquelle elles ont été créées. 

Cette organisation simple voir simpliste peut-être démultipliée sur de multiples couches en fonction de la complexité du projet. 

> L'idée importante à retenir est qu'une organisation rigoureuse de vos branches peut vous aider dans la stabilité de vos développements et de vos projets. c'est ce à quoi fait appel la notion de branches de stabilité progressive.

Nous ne rentrerons pas dans les détails des multiples scénarios possibles si vous souhaitez avoir une vue plus détaillée de cet aspect vous pouvez vous reporter au lien suivant : https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows

# Interaction des branches locales et distantes

Nous avons déjà aborder rapidement les notions de fetch / push / et de tracking des branches, arrêtons-nous quelque peu sur ces outils. 

Lorsque vous clonez un remote vous le clonez dans son dernier état (son dernier commit). 

Si ce remote évolue, tant que vous ne faites pas une synchronisation de ce remote vous restez dans l'état de ce dernier commit connu. Pour vous synchroniser avec les modifications de ce remote vous devez faire un `git fetch <remote>/<branch>` ou remote est le shortname d'un remote et branch la branche concernée par la récupération de data sur ce dépôt distant. 

Ainsi à chaque fois que vous allez fetcher une branche remote celle ci sera updaté dans votre dépôt local. Il est également possible de fetcher tout un remote, sans préciser de branche avec la commande `git fetch <remote>`.

La commande de type "push" agit exactement de la même manière avec la même syntaxe mais cette fois en poussant vos modifications vers le remote. La prochaine fois que vos collaborateurs feront un fetch ils pourront ainsi bénéficier de vos évolutions. 

Il existe également les raccourcis `git pull` et `git push` sans argument. Pour pouvoir les utiliser nous devons nous attarder sur la notion de tracking des branches. Le tracking va établir un lien direct entre une branche locale et une branche distante. L'établissement de ce lien permettra d'utiliser les commandes push et pull sans préciser la branche à laquelle nous faisons référence ni le dépôt. La branche qui est trackée est appelée "upstream branch". 

Pour établir ce lien de tracking vous pouvez utiliser la commande suivante `git checkout --track <REMOTE>/<BRANCH>`, si vous essayez de checkout une branche qui : 
 * n'existe pas
 * ET
 * qui existe sur seulement un remote

Alors ce checkout va agir comme un raccourci vers la commande vue précédemment. 

Vous pouvez également utiliser la commande `git branch -u <REMOTE>/<BRANCH>` pour setter le tracking d'une branche déjà existante localement ou le modifier. 

Enfin la commande `git branch -vv` vous permet d'identifier toutes les branches locales et les branches distantes suivies. 

Nous avons précédemment défini la commande `git pull` comme un raccourci, mais elle a une différence majeure avec un `git fetch` : le fetch ne modifie pas votre working directory, il se contente de récupérer tous les changements sur le serveur distant. La commande `git pull` réalise un fetch mais merge également le contenu du remote. Ainsi que nous utilisions fetch puis merge ou git pull nous réalisons essentiellement la même chose.  

Dernier point de ces interactions lorsqu'une branche distante n'a plus d'utilité il est possible de la supprimer en utilisant la commande `git push <REMOTE> --delete <NOM BRANCHE>`

[^1]: Se reporter au chapitre 1 partie 4
