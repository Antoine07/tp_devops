# Définition du déploiement (d'applications / sites)

Commençons par définir ce qu'est le déploiement dans le cadre d'une application : 

>Déployer une application ou un site web signifie appliquer un procédé permettant d'installer ou mettre à jour le site web sur un environnement donné.
>
>[...]
>
>Dans cet exemple, l’environnement de développement est votre machine locale, l’environnement de test votre serveur, et l’environnement de production l’hébergement du client.
>
>*Source : https://www.blogduwebdesign.com/deployer-son-application-en-production-les-bonnes-methodes-a-connaitre/*

Que nous apprend cette définition ?

Tout d'abord que le déploiement est un procédé, ou process en anglais. Il va donc comprendre un certain nombre de règles et de comportements automatisés. Autre élément important le déploiement est lié à un environnement. On déploie vers un environnement de test ou de production. 

Intéressons-nous maintenant à l'outil que nous allons étudier à savoir jenkins et sa définition tirée du site officiel : 

> The leading open source automation server, Jenkins provides hundreds of plugins to support building, deploying and automating any project.

Jenkins se décrit comme un automation server. Il reprend donc bien la notion d'automatisation que nous avons vu précédemment (je passe ici sur le côté open source, qui n'est pas un distinctif). Il propose en revanche une distinction entre trois éléments inclus dans le déploiement : 

1) Building
2) Deploying
3) Automating

Cette distinction tri-partite est très intéressante. L'action de "build" est une action qui consiste à rendre votre application utilisable. Par exemple si vous faites de l'angular un build va transposer les méta fichiers d'angular qui vous servent au code en fichier js/html qui servent du côté client à l'interprétation, c'est donc une étape fondamentale de préparation du déploiement.

Le déploiement lui-même consiste à rendre disponible dans l'environnement de production l'app qui a été build. Il inclue la copie sur les serveurs des fichiers nécessaires, leur amendement si nécessaire etc. 

La phase d'automatisation est quant à elle plus large, elle peut comprendre par exemple des tests qui ont pour vocation de s'assurer du bon comportement dans l'environnement cible. 

Dans les avantages de Jenkins sur le site officiel toujours nous retrouvons les éléments suivants qui nous aident à préciser la ou les vocations de jenkins : 

> Continuous Integration and Continuous Delivery
>
>As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any project.

Easy installation

Jenkins is a self-contained Java-based program, ready to run out-of-the-box, with packages for Windows, Linux, macOS and other Unix-like operating systems.
Easy configuration

Jenkins can be easily set up and configured via its web interface, which includes on-the-fly error checks and built-in help.
Plugins

With hundreds of plugins in the Update Center, Jenkins integrates with practically every tool in the continuous integration and continuous delivery toolchain.
Extensible

Jenkins can be extended via its plugin architecture, providing nearly infinite possibilities for what Jenkins can do.
Distributed

Jenkins can easily distribute work across multiple machines, helping drive builds, tests and deployments across multiple platforms faster.
