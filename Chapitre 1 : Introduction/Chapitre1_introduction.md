# Introduction

Dans cette introduction nous avons particulièrement suivi les élements introductifs du livre "The entire Pro Git book"[^1]

## Définition d'un système de contrôle de versions

> Un logiciel de gestion de versions (ou VCS en anglais, pour version control system) est un logiciel qui permet de stocker un ensemble de fichiers en conservant la chronologie de toutes les modifications qui ont été effectuées dessus. Il permet notamment de retrouver les différentes versions d'un lot de fichiers connexes.[^2]

## Local Version Control Systems vs Centralized Version Control Systems vs Distributed Version Control Systems

### Local Version Control Systems (LVCS):

C'est le système de versioning le plus primitif et que nous avons tous fait intuitivement. Il consiste à copier un fichier ou un dossier puis d'enregistrer chaque version du fichier dans un dossier différent ou avec un nom différent. 

Néanmoins, l'inconvénient majeur de ce genre de système est la propension à faire des erreurs. Lors de l'enregistrement l'utilisateur peut se tromper de nom et donc écraser des modifications. 

Pour éviter ce genre d'erreurs, il y a très longtemps un premier système de gestion des versions est apparu. Il conservait dans une database locale toutes les modifications successives des fichiers.

Le système le plus populaire de ce type était appelé "RCS".

![image](https://user-images.githubusercontent.com/98811386/169887864-efc66478-2594-4894-9e22-7fa843c30ca1.png)

### Centralized Version Control Systems (CVCS).

Le problème majeur d'un système LVCS est l'absence de possibilité de collaboration. Etant donné que le système de versions est stocké localement il n'est pas facilement partageable. Pour contrer cette problématique, des systèmes dits de CVCS sont apparus. 

Ces systèmes contiennent un serveur centralisé qui contient tous les fichiers et un certain nombre de clients qui vont récupérer les sources depuis ce système centralisé. 

![image](https://git-scm.com/book/en/v2/images/centralized.png)

Comparativement aux LVCS ce système offre des avantages certains : 

* Le partage des évolutions de chaque fichier suivi est rendu possible pour de multiples utilisateurs.
* Il est plus facile pour les administrateurs de suivre ce que chacun produit, et des droits de chacun pour la modification.
* Il est beaucoup plus facile d'administrer une seule base de données centralisées, que des dizaines sur des postes locaux. 

Néanmoins ce type de système a aussi des défauts majeurs : 

* La présence de l'historique de modifications sur un serveur unique entraîne un grand risque de perte de données en cas de défaillance ou d'indisponibilité du serveur. 
* L'utilisateur ne télécharge que la dernière version qui est une sorte de canon et écrase toutes les versions précédentes.

Les CVCS les plus célèbres sont : CVS, Subversion, and Perforce

### Distributed Version Control System (DVCS)

Pour répondre à cet inconvénient majeur, le DVCS va apporter une évolution supplémentaire. Au lieu de télécharger uniquement la dernière version, les utilisateurs d'un DVCS téléchargent non seulement l'état du code actuel mais également l'état de toutes les versions successives. 

Chaque utilisateur récupère donc un miroir complet du dépôt, de ses modifications successives, et de l'état de chaque fichier dans le temps. On peut donc assimiler ce que récupère un utilisateur à un clône du dépot.

> Zoom sur la notion de dépot : Le but principal d'un dépôt est de stocker un ensemble de fichiers ainsi que l'historiques des modifications apportés aux fichiers.[^3]

![image](https://git-scm.com/book/en/v2/images/distributed.png)

Les avantages liés à cette méthode sont les suivants : 

* Chaque utilisateur possède une copie complète du serveur qui contient le dépôt. Il peut donc devenir la source de la restauration de ce serveur même en cas de défaillance de ce dernier. 
* Autre avantage : Il est possible de collaborer avec différents groupes de personnes et à différents endroits du projet simultanément. Cela permet de créer des modèles de collaboration impossibles avec des systèmes centralisés, comme les modèles hiérarchiques. 

Les CVCS les plus connus sont : Git, Mercurial, Bazaar ou Darcs

## Historique de git

L'histoire de git est étroitement liée à celle de la communauté linux :
* Entre 1991 et 2002 la maintenance du kernel linux utilisait un système maison qui stockait les modifications sous forme de patchs et fichiers archivés 
* En 2002 les responsables de la maintenance décident d'utiliser un logiciel propriétaire appelé BitKeeper.
* En 2005 les relations avec BitKeeper sont dégradés et la société éditant BitKeeper, elle décide alors de rendre BitKeeper payant. 
* La décision sera prise du côté linux de créer son propre logiciel (git !).

La confection de ce logiciel doit répondre aux besoins rencontrés lors de l'utilisation de BitKeeper :
* Vitesse.
* Simplicité du design.
* Possibilité de supporter des développements parallèles, aussi appelés "non linéaires". (Nous verrons plus en avant le système dit de branching qui soutient ce paradigme).
* Gestion distribuée des dépôts.
* Capable de gérer des projets d'ampleur (en terme de vitesse et de taille de la data)

L'évolution de git est donc continue et suit ces principes depuis 2005. 

## Définition de git

### Le rapport de git à la data 

La différence majeure de git est la façon dont git conçoit de la data. 

> Les systèmes classiques de versioning pensent la data comme un listing de changements de fichiers individuels, et enregistre à chaque version le fichier qu'il soit modifié ou non, selon le schéma suivant (on appelle cette méthode la méthode "delta-based". 

![image](https://git-scm.com/book/en/v2/images/deltas.png)

> Git ne réfléchit pas de la même façon, il voit plutot les versions enregistrées successivement comme un instantané (snapshot) de l'état de l'ensemble du système de fichier. 
> Ainsi à chaque fois que l'on enregistre l'état d'un dépôt git prend une photo de l'état actuel et de l'état à sauvegarder. Un fichier non modifié ne sera pas alors réenregistré, au lieu de cela il sera linké à l'état précédent. 
> Git se définit donc lui-même comme un "stream de snapshot", ou en français une succession d'instantanés.

![image](https://git-scm.com/book/en/v2/images/snapshots.png)


[^1]: Source : https://git-scm.com/book/en/v2
[^2]: Source : https://fr.wikipedia.org/wiki/Logiciel_de_gestion_de_versions
[^3]: Source : https://en.wikipedia.org/wiki/Repository_(version_control)
