# Le plugin Maven

## Pourquoi Maven ? 

Maven est un outil qui présente de multiples avantages pour commencer à utiliser jenkins. 

Tout d'abord il dispose d'un plugin opensource qui gère entièrement les projets Maven 2 et 3. 

Ce plugin fournit une série d'avantage concernant l'utilisation de Maven : 

* Il ajoute un nouveau job "Maven Project" qui réduit grandement les tâches de configuration pour un projet Maven.
* Il dispose d'artefacts définis à la suite du déploiement qui nous permettront d'utiliser des fonctionnalités avancées de Jenkins.
* Il dispoose de reportings sur les tests, ce qui là aussi nous permettra d'aborder cette facette. 
* Il permet également des builds incrémentaux, ce qui réduit le poids sur les ressources. 
* Il permet des builds parallèles et distribués entre les exécuteurs jenkins.  
* Il permet de créer des chaînes de dépendances entre les builds et d'exécuter des sous builds dont est dépendant le build parent. 

## Installation du plugin Maven 

Pour installer et configurer le plugin maven nous allons nous rendre dans Administrer Jenkins > Configuration globale des outils. 

![Capture d’écran de 2022-06-01 23-09-04](https://user-images.githubusercontent.com/98811386/171502329-36357386-62d0-482c-a824-575cf43118f2.png)

Nous allons ensuite scroller dans cette section jusqu'à maven puis le configurer comme suit : 

![Capture d’écran de 2022-06-01 23-12-02](https://user-images.githubusercontent.com/98811386/171502781-ce8da568-377b-45a4-aa8d-333a877a5481.png)

Rien ne se passe à ce moment mais maven sera installé lors du premier build sur cette instance de jenkins. 

Nous allons maintenant nous rendre dans Administrer Jenkins > Gestion des plugins. 

Nous cliquerons alors sur "disponibles" puis tapperons Maven Integration. 

![Capture d’écran de 2022-06-01 23-14-38](https://user-images.githubusercontent.com/98811386/171503151-11c9de64-c425-40d5-8937-ec083a05d492.png)

Nous allons ensuite cliquer pour sélectionner le plugin, puis sur "Install without restart"

La confirmation de l'installation devrait produire cet écran :

![Capture d’écran de 2022-06-01 23-16-21](https://user-images.githubusercontent.com/98811386/171503433-8dd37b8d-f51c-45a4-8f98-a384189ac030.png)

En bas de la page d'installation nous allons choisir "Redémarrer Jenkins quand l'installation est terminée et qu'aucun job n'est en cours".

Si l'on se rend maintenant sur la page "Nouveau Item", on peut se rendre compte qu'un nouveau job Maven est disponible : 

![Capture d’écran de 2022-06-01 23-19-44](https://user-images.githubusercontent.com/98811386/171503819-199a3b1c-2633-4ab9-a1b8-6a0f666ef08d.png)

# Construction du premier projet Maven. 

Nous allons maintenant créer un projet maven ayant pour nom test Maven. 
