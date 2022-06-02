# Définition et utilité des pipelines. 

Les builds complexes et les process de release longs peuvent être difficiles à gérer avec uniquement des freestyle jobs. 

Les pipelines jenkins permettent de mettre en oeuvre un set important de plugins jenkins qui permettent la réalisation de ces process complexes. 

Les pipelines jenkins sont écrits en "Groovy code" et sont placés dans un fichier appelé "jenkinsfile". 

Les avantages apportés par la gestion des pipelines sont les suivants : 

* L'incorporation dans un fichier de type jenkinsfile rend possible la traçabilité des changements de pipeline car il figure dans une code database.
* Cette traçabilité entraîne un contrôle plus important. 
* Les pipelines existent indépendamment de la sessions jenkins. Si par accident la session jenkins est détruite vous pouvez toujours la reconstruire facilement et garder les pipelines existants.
* Les pipelines sont également par définition facilement extensibles par le biais de plugin ou de librairies partagées. 
* Du fait d'être issu d'un langage de programmation les jenkinsfile supporte des éléments logiques comme les conditions, les boules et les exécutions parallèles.

Définitions liées aux pipelines[^1] : 

> Pipeline : User-defined model of a build, test, and release process for a software product.

> Node : A machine that the jenkins controller can execute pipeline on.

> Stage : A logical grouping of steps that typically align with the build, test and release portions of the software development lifecycle.

> Steps : Individual tasks completed within a stage of a pipeline (such as invoking a node's shell and executing a command such as `ls` or `mkdir` on it).

> Declarative pipelines : Newer feature of Jenkins Pipeline. They have richer syntactical features. Declarative pipelines make reading and writing pipelines easier. 

[^1]: Source : https://www.youtube.com/watch?v=nCKxl7Q_20I

# Création de notre premier pipeline

Toujours dans l'optique de simplifier notre rapport aux notions de jenkins nous allons installer le plugin 

Une fois le plugin installé nous allons nous rendre dans Nouveau item puis créer un job de type pipeline que l'on nommera Maven pipeline test. 

Nous allons nous rendre dans la section pipeline, nous verrons plus tard que pour tirer pleine partie de la puissance des pipelines nous devons les commiter dans un système de versioning. Pour l'instant on sélectionne l'option "pipeline script" afin de nous familiariser avec les pipelines avant de  les inclure dans un contrôle de version. 

![Capture d’écran de 2022-06-02 21-29-57](https://user-images.githubusercontent.com/98811386/171723256-e838b3ae-0aeb-4cc6-8030-50b2992b7e03.png)

