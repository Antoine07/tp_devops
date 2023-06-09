# Aperçu de l'interface. 

## La home

Par défaut l'interface que vous voyez doit être celle-ci : 

![Capture d’écran de 2022-06-01 22-13-33](https://user-images.githubusercontent.com/98811386/171493252-5ffeb4fb-0bc3-4588-a437-b9426a50285c.png)

Dans la section "Commencer à créer votre projet" vous pouvez voir la mention "Créer un job". 

Dans jenkins tout est "job", il faut comprendre par job une tâche automatisée, rappelons que jenkins est avant tout un logiciel d'automatisation. Il existe plusieurs types de job, pour les voir il faut cliquer sur "Nouveau Item". Vous verrez alors apparaître la fenêtre suivante : 

## La page Nouveau item

![Capture d’écran de 2022-06-01 22-16-03](https://user-images.githubusercontent.com/98811386/171493611-1ee0cf2b-7954-4d20-8f5a-9a13b626db26.png)

Détaillons un peu ces différents types de job :

* Projet free-style : Dédié aux projets de faible envergure avec peu de tests ou d'étapes dans le build. Il s'agit en général d'applications simples avec une organisation simple de la database de code. 
* Pipeline : Dédié aux projets de plus grandes envergures avec des workflows plus complexes et plus d'étapes de tests et déploiements. 
* Projet multi-configuration : Dédié aux cas où les plateformes de déploiement sont multiples par exemple un projet déployé sur IOS et Android
* Folder : Sert uniquement à grouper les différents jobs
* Organization Folder : Permet de récuperer les repo d'une organisation sur github, et va créer des jobs automatiquement si il y a un jenkins file. 
* Pipeline Multibranche : Permet de définir une base de code (autre que github) et va créer des jobs automatiquement à partir des jenkins file dans chaque branche. 

## La page administrer Jenkins

![Capture d’écran de 2022-06-01 22-27-20](https://user-images.githubusercontent.com/98811386/171495667-7c08b5fa-ec5c-4a9a-bb9d-dfed090499dd.png)

La page d'administration de Jenkins est le coeur de sa configuration. 

### La section configurer le système 

Section centrale dans jenkins, elle permet comme son nom l'indique de configurer jenkins lui-même mais aussi la plupart des plugins. 

L'un des paramètres a considérer est le nombre d'exécuteurs, il s'agit du nombre de jobs qui peuvent tourner simultanément sur jenkins. Attention à ne pas trop l'augmenter sinon l'impact sur la performance de votre serveur va être énorme (cpu, ram ...)

Un autre paramètre à noter est ce lui du répertoire de jenkins, ce dernier va être le centre de stockage pour jenkins c'est ici qu'il copiera tous les fichiers dont il a besoin, ainsi que toutes les datas nécessaires. 

### La section configuration globale des outils

Cette section permet de spécifier les installations des différents outils nécessaires à l'exécution des jobs jenkins, les éléments comme git les jdk et autres éléments nécessaires. 

### La section gestion des plugins

Comme son nom l'indique elle permet d'ajouter, modifier et updater des plugins. 

### Configurer la sécurité globale 

Dans cette section vous pourrez configurer la sécurité de jenkins et notamment les méthodes d'authentification. Généralement dans les entreprises vous utiliserez des méthodes de type LDAP, dans le cadre de cette démonstration nous allons utiliser la propre database de jenkins pour gérer notre user. 

Il est également possible de gérer les autorisations des différents users à ce niveau. 

### Manage credentials

Permet de gérer un trousseau d'accès pour les différents outils qui seront en communication avec jenkins, dans notre exemple il s'agira des outils de type github. 

Par exemple jenkins va avoir besoin d'une clé ssh pour cloner les éléments de la database de code si le dépôt est privé. Elle sera stockée ici. 
