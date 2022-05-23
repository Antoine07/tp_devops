# Initialisation ou récupération d'un repository

Il existe deux façons de débuter avec git : 

* Initialiser un repository git dans un dossier déjà existant localement
* Cloner un dépôt distant. 

## Initialisation d'un repository.

Dans le cadre de cet exercice nous allons initialiser un dépôt git à partir d'un dossier existant. 

* Créez un dossier gitTp.
* Déplacez-vous dans ce dossier et créez un fichier html basique avec un hello world et une feuille de style css vide nommée elle aussi helloworld.css. 
* Entrez la commande `git init` 

Vous devriez alors avoir un retour de ce type :

* Dépôt Git vide initialisé dans `chemin/gitTp/.git/`

Ce retour signifie que git a créé un sous dossier .git contenant tous les éléments d'un squelette vide de git. 

A ce stade nous allons utiliser la commande `git status`. Cette dernière nous donne un suivi des différents états des dossiers et fichiers suivis. Dans notre cas nos deux fichiers ne sont pas suivis et apparaissent donc en rouge et précédés de la mention suivante:

>Fichiers non suivis: (utilisez "git add <fichier>..." pour inclure dans ce qui sera validé)

Ainsi dans le workflow nous devons maintenant ajouter les fichiers au suivi.

Dans notre cas nous souhaitons que chaque élément déjà présent à ce moment dans le dossier gitTp soit suivi, à savoir notre fichier html et notre fichier css. Pour cela nous allons utiliser la commande `git add .`

Arrêtons nous sur cette commande quelques instants. Elle a permis d'enclencher le suivi de modification des deux fichiers. Ils seront désormais suivis et à chaque commit leur état sera enregistré. Il est à noter que l'on peut aussi préciser des dossiers ou fichiers spécifiques à suivre. Il est enfin à noter que tout nouveau fichier ou dossier créé devra d'abord être ajouté via cette commande. 

Nous allons maintenant réeffectuer la commande `git status`. Les deux fichiers apparaissent cette fois en vert avec la mention 

>Modifications qui seront validées : (utilisez "git rm --cached <fichier>..." pour désindexer)
>
> nouveau fichier : helloworld.css
>
> nouveau fichier : helloworld.html



Dernier point pour créer un nouvel instantané (snapshot) localement nous allons exécuter la commande `git commit`. 

Lors de l'exécution de `git commit` l'éditeur de texte définit précédemment va se lancer, il faudra alors enregistré une description du commit. Il est possible d'enregistrer directement un message en utilisant le modificateur `git commit -m 'ceci est un message de commit d'exemple'`.

Le commit initial va alors créer une première image instantanée ou snapshot, à partir de celle ci toute modification des éléments trackés sera prise en considération comme nous le verrons plus tard. 

Une dernière exécution de la commande `git status` vous donnera la sortie suivante :
>Sur la branche master
>
>rien à valider, la copie de travail est propre

On voit donc maintenant que tous nos fichiers sont exactement tels qu'ils étaient à la version précédente. 
  
On notera également que la commande git status nous donne la branche actuelle utilisée. 
 
## Clonage d'un repository
  
Si vous souhaitez copier un dépôt git existant la commande `git clone` va vous permettre de réaliser cette action. 

Ce que va faire cette commande c'est copier localement l'ensemble d'un dépôt git, incluant les fichiers eux-mêmes mais aussi l'ensemble de l'historique de modification comme déjà vu précédemment. Pour décomposer cette commande, elle va donc créer un dossier ayant pour nom celui du projet git que vous clonez. Elle va ensuite créer et initialiser un répertoire `.git`, va récupérer toute la data pour ce dépôt, puis va finalement récupérer l'image de la derniere version de ce dépôt. 

La composition exacte de la commande git clone est la suivante :

> git clone \<url\>

\<url\> peut prendre trois types de valeur : 
* Une url sous protocole `https://` par exemple https://github.com/testdepot
* `git://` qui permettra de récupérer également un dépôt git
* ou encore `user@server:path/to/repo.git`
  
Chacune de ces trois méthodes d'appel ayant le même résultat.

# Effectuer des changements sur un dépôt git
  
Le but d'un dépôt git est bien entendu d'être évolutif, pour cela il faut se rappeler les points capitaux des 3 états vus précédemment ainsi que la notion de tracking ou non tracking des différents fichiers.


  
