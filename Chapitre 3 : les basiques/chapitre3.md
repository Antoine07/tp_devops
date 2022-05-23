# Les basiques de git

## Initialisation ou récupération d'un repository

Il existe deux façons de débuter avec git : 

* Initialiser un repository git dans un dossier déjà existant localement
* Cloner un dépôt distant. 

### Initialisation d'un repository.

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

>Modifications qui seront validées :
>
>   (utilisez "git rm --cached <fichier>..." pour désindexer)
>
>       nouveau fichier : helloworld.css
>
>       nouveau fichier : helloworld.html
