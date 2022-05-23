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

Pour répondre à cet inconvénient majeur, le DVCS va apporter une évolution supplémentaire. Au lieu de télécharger uniquement la dernière version, les utilisateurs d'un DVCS téléchargent non seulement l'état du code actuel mais également l'enregistrement de toutes les versions successives. 


[^1]: Source : https://git-scm.com/book/en/v2
[^2]: Source : https://fr.wikipedia.org/wiki/Logiciel_de_gestion_de_versions
