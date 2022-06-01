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

# Jenkins, rôles buts et fonctionnement théorique

Intéressons-nous maintenant à l'outil que nous allons étudier à savoir jenkins et sa définition tirée du site officiel : 

> The leading open source automation server, Jenkins provides hundreds of plugins to support building, deploying and automating any project.

Jenkins se décrit comme un automation server. Il reprend donc bien la notion d'automatisation que nous avons vu précédemment (je passe ici sur le côté open source, qui n'est pas un distinctif). Il propose en revanche une distinction entre trois éléments inclus dans le déploiement : 

1) Building
2) Deploying
3) Automating

Cette distinction tri-partite est très intéressante :
* L'action de "build" est une action qui consiste à rendre votre application utilisable. Par exemple si vous faites de l'angular un build va transposer les méta fichiers d'angular qui vous servent au code en fichier js/html qui servent du côté client à l'interprétation, c'est donc une étape fondamentale de préparation du déploiement.

* Le déploiement lui-même consiste à rendre disponible dans l'environnement de production l'app qui a été build. Il inclue la copie sur les serveurs des fichiers nécessaires, leur amendement si nécessaire etc. 

* La phase d'automatisation est quant à elle plus large, elle peut comprendre par exemple des tests qui ont pour vocation de s'assurer du bon comportement dans l'environnement cible. 

Dans les avantages de Jenkins sur le site officiel toujours nous retrouvons les éléments suivants qui nous aident à préciser la ou les vocations de jenkins : 

> Continuous Integration and Continuous Delivery
>
>As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any project.

Cet élément nous donne deux possibilités de jenkins, soit il agit comme un simple serveur d'intégration continue, soit comme une suite de livraison continue. 

Arrêtons-nous sur ces éléments pour mieux comprendre la distinction.

> L'intégration continue est un ensemble de pratiques utilisées en génie logiciel consistant à vérifier à chaque modification de code source que le résultat des modifications ne produit pas de régression dans l'application développée. [..]Le principal but de cette pratique est de détecter les problèmes d'intégration au plus tôt lors du développement. De plus, elle permet d'automatiser l'exécution des suites de tests et de voir l'évolution du développement du logiciel.
>
>L'intégration continue est de plus en plus utilisée en entreprise afin d'améliorer la qualité du code et du produit final2.[^1] 

Voici en contraste une définition de la livraison continue

> La livraison continue (CD, Continuous Delivery) est une approche de la publication de logiciels dans laquelle les équipes de développement produisent et testent le code dans des cycles courts, en s'appuyant généralement sur une plus grande automatisation.
>
> Ce processus permet de créer, tester et déployer des logiciels rapidement en privilégiant des mises à jour incrémentielles, au lieu de refontes complètes.
>
> La livraison continue vise à raccourcir au maximum les boucles de rétroaction, afin d'améliorer la qualité des logiciels. Le code est livré à intervalles réguliers pour être soumis à des tests d'acceptation (UAT, User Acceptance Testing, aussi appelés Bêta tests), ou essayé dans l'environnement de test, afin de mettre en évidence les causes et les effets.[^2]

On voit donc que jenkins intervient sur ces deux pans en permettant des process d'automatisation qui visent à réduire l'erreur humaine au maximum. 

> Easy configuration
>
>Jenkins can be easily set up and configured via its web interface, which includes on-the-fly error checks and built-in help.

On voit donc que jenkins permet également l'automatisation de tests, notamment lors des builds, l'ensemble est géré par une interface web, ce qui rentre dans une logique dev-ops. 

>Plugins
>
>With hundreds of plugins in the Update Center, Jenkins integrates with practically every tool in the continuous integration and continuous delivery toolchain.

Cette section fait référence à l'intégration de jenkins dans les stacks d'intégration et livraison continues. En clair avec jenkins et ses plugins vous pouvez aller plus loin qu'un déploiement simple pour intégrer les logiques de testing que nous avons précédemment vu dans l'organisation de git. 

> Distributed
>
> Jenkins can easily distribute work across multiple machines, helping drive builds, tests and deployments across multiple platforms faster.

Les architectures techniques modernes sont plus complexes que les anciennes, elles incluent du cloud ou de multiples machines et un outil de déploiement doit donc prendre en compte ces différents contextes. 

Jenkins répond à deux besoins primordiaux des developpeurs : 
 - Les développeurs veulent que leurs changements de code soient surs, ils développent en parallèle et veulent être surs que leur développement n'entraîne pas d'erreurs. L'intégration manuelle ne se fait pas selon une fréquence et prend du temps, jenkins automatise cela.
 - Les développeurs ont besoin que leurs changements soient testés dans un environnement standardisé. Jenkins fournit un environnement standardisé qui permet de linéariser ces problématiques. 

Jenkins agit sur deux étapes cruciales du software développement : le testing et le déploiement.

Voici un schéma type du fonctionnement de jenkins : 

![Capture d’écran de 2022-06-01 21-47-46](https://user-images.githubusercontent.com/98811386/171489238-4487de2c-02b1-4d04-acc9-678ce96fd359.png)

*Source : https://www.youtube.com/watch?v=nCKxl7Q_20I*



[^1]: Source : https://fr.wikipedia.org/wiki/Int%C3%A9gration_continue
[^2]: Source : https://www.lemagit.fr/definition/Continuous-Delivery
