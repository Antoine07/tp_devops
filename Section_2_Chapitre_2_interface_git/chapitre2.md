# Premier aperçu de l'interface. 

Par défaut l'interface que vous voyez doit être celle-ci : 

![Capture d’écran de 2022-06-01 22-13-33](https://user-images.githubusercontent.com/98811386/171493252-5ffeb4fb-0bc3-4588-a437-b9426a50285c.png)

Dans la section "Commencer à créer votre projet" vous pouvez voir la mention "Créer un job". 

Dans jenkins tout est "job", il faut comprendre par job une tâche automatisée, rappelons que jenkins est avant tout un logiciel d'automatisation. Il existe plusieurs types de job, pour les voir il faut cliquer sur "Nouveau Item". Vous verrez alors apparaître la fenêtre suivante : 

![Capture d’écran de 2022-06-01 22-16-03](https://user-images.githubusercontent.com/98811386/171493611-1ee0cf2b-7954-4d20-8f5a-9a13b626db26.png)

Détaillons un peu ces différents types de job :

* Projet free-style : Dédié aux projets de faible envergure avec peu de tests ou d'étapes dans le build. Il s'agit en général d'applications simples avec une organisation simple de la database de code. 
* Pipeline : Dédié aux projets de plus grandes envergures avec des workflows plus complexes et plus d'étapes de tests et déploiements. 
* Projet multi-configuration : Dédié aux cas où les plateformes de déploiement sont multiples par exemple un projet déployé sur IOS et Android
* Folder : Sert uniquement à grouper les différents jobs
* Organization Folder : Permet de récuperer les repo d'une organisation sur github, et va créer des jobs automatiquement si il y a un jenkins file. 
* Pipeline Multibranche : Permet de définir une base de code (autre que github) et va créer des jobs automatiquement à partir des jenkins file dans chaque branche. 
