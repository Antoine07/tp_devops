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

da