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

Nous allons ensuite cliquer sur le lien Pipeline syntax afin de générer automatiquement notre premier code pipeline. 

Lorsque vous arrivez sur le pipeline generator vous allez dans un premier temps entre dans le snippet generator. Ce snippet generator vous permet de générer facilement des steps particuliers (cf définition du step plus haut). 

![Capture d’écran de 2022-06-02 21-35-26](https://user-images.githubusercontent.com/98811386/171723863-746bcbe0-b945-4606-b184-923065a35900.png)

Le menu déroulant fourni la liste des steps disponibles, puis il faut ensuite configurer selon le step ce que l'on veut. La en l'occurrence je veux archiver un artefact nommé build, il suffit de cliquer sur "Generate pipeline script" et voilà vous disposez d'un morceau de code pipeline !

Si maintenant nous souhaitons générer un pipeline plus complet nous allons cliquer sur "Declarative directive generator". Cela va nous permettre de générer notre premier pipeline complet. 

![Capture d’écran de 2022-06-02 21-38-04](https://user-images.githubusercontent.com/98811386/171724262-308c195a-185d-404f-9b57-10d2c3113428.png)

Si vous regardez la structure de cette page elle est semblable à la précédente, on sélectionne une directive puis on la configure et on génère le code. 

Dans notre cas nous souhaitons définir plusieurs stages (cf définition précédente) successifs, nous choisissons donc l'option Stage:Stages puis nous ajoutons notre premier stage.  

![Capture d’écran de 2022-06-02 21-40-49](https://user-images.githubusercontent.com/98811386/171724749-550e4f90-55f2-4781-a5c7-dba6f7174d65.png)

Le premier stage que nous allons définir est le stage de "build" qui aura la responsabilité de build le code depuis notre codebase. 

Le stage peut contenir plusieurs type d'éléments dont des stages en parallèle, pour l'instant nous allons rester simple et faire contenir des steps à notre stage. 

Nous pouvons également ajouter des élements particuliers à la gestion de ces steps comme un Agent ou encore un environnement ou des conditions ou options. Toujours pour une raison de simplicité, nous n'allons pas ajouter d'options particulières. 

Une fois ce stage créé nous allons en ajouter deux autres sur le même model "test" et "deploy". La logique sera que le build se déroule puis si les tests sont réussis alors on déploiera la mise à jour. 

```groovy
stages {
  stage('build') {
    steps {
      // One or more steps need to be included within the steps block.
    }
  }

  stage('test') {
    steps {
      // One or more steps need to be included within the steps block.
    }
  }

  stage('deploy') {
    steps {
      // One or more steps need to be included within the steps block.
    }
  }

}
```
