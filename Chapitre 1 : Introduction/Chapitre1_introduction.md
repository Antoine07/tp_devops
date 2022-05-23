# Introduction

Dans cette introduction nous avons particulièrement suivi les élements introductifs du livre "The entire Pro Git book"[^1]

## Définition d'un système de contrôle de versions

> Un logiciel de gestion de versions (ou VCS en anglais, pour version control system) est un logiciel qui permet de stocker un ensemble de fichiers en conservant la chronologie de toutes les modifications qui ont été effectuées dessus. Il permet notamment de retrouver les différentes versions d'un lot de fichiers connexes.[^2]

## Local Version Control Systems vs Centralized Version Control Systems vs Distributed Version Control Systems

### Local Versions Control Systems (LVCS):

C'est le système de versioning le plus primitif et que nous avons tous fait intuitivement. Il consiste à copier un fichier ou un dossier puis d'enregistrer chaque version du fichier dans un dossier différent ou avec un nom différent. 

Néanmoins, l'inconvénient majeur de ce genre de système est la propension à faire des erreurs. Lors de l'enregistrement l'utilisateur peut se tromper de nom et donc écraser des modifications. 

Pour éviter ce genre d'erreurs, il y a très longtemps un premier système de gestion des versions est apparu. Il conservait dans une database locale toutes les modifications successives des fichiers.

Le système le plus populaire de ce type était appelé "RCS".

![image](https://user-images.githubusercontent.com/98811386/169887864-efc66478-2594-4894-9e22-7fa843c30ca1.png))

### Centralized Versions Control Systems (CVCS).

Le problème majeur d'un système LVCS est l'absence de possibilité de collaboration. Etant donné que le système de versions est stocké localement il n'est pas facilement partageable. Pour contrer cette problématique, des systèmes dits de CVCS sont apparus. 

Ces systèmes contiennent un serveur centralisé qui contient tous les fichiers 


[^1]: Source : https://git-scm.com/book/en/v2
[^2]: Source : https://fr.wikipedia.org/wiki/Logiciel_de_gestion_de_versions
