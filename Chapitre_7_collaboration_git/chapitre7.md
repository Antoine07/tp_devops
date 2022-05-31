# Les différents workflows distribués

## Worflows centralisés

Les workflows centralisés sont directement inspirés des CVCS que nous avons vu précédemment. 

Dans cette vision il existe un hub central qui peut accepter du code et chaque développeur synchronise son travail avec ce hub central. Chacun des développeurs est vu comme un "consumer" du hub et se synchronise avec cette instance centrale sans avoir de relations directs avec les autres. 

![image](https://git-scm.com/book/en/v2/images/centralized_workflow.png)
*Source : https://git-scm.com/book/en/v2/images/centralized_workflow.png

Dans cette vision chaque modification doit etre séquentielle si le développeur A envoie vers le shared repository, le développeur B devra d'abord pull le travail du développeur A puis ensuite pusher son propre travail.

Le système de branches permet d'utiliser ce genre de worklow même dans des équipes de très grande taille travaillant chacune sur des dizaines voire des centaines de branches en simultané. 

## Integration manager workflow

Git autorise le fait d'avoir de multiples repository distants. Dès lors cela autorise de nouvelles organisations des workflows et de faire en sorte que chaque développeur ne soit pas un simple consumer mais aussi un hub. 

Dans le scénario que nous allons voir maintenant un certain nombre de prérequis sont à comprendre : 

- Le scénario implique un dépôt canonique qui représente le projet officiel. 
- A partir de ce dépôt canonique chaque développeur va cloner son propre dépôt public et va pusher les changements vers celui-ci
- Lorsque les changements sont satisfaisants on demande au manager du dépôt canonique de puller ces modifications
- Le manager du dépôt canonique ajoute alors le dépôt public du développeur comme un remote et intègre les modifications localement
- Le manager du dépôt pousse les modifications vers le dépôt canonique. 

Ce système est le plus commun dans les outils comme github. La création de fork permet de pousser vers votre fork les changements et de les décorreler de leur intégration dans le projet principal. Chacun peut avancer a son rythme, et le manager décidera ou non d'intégrer ce dépôt à son propre rythme. 

![image](https://git-scm.com/book/en/v2/images/integration-manager.png)
*Source : https://git-scm.com/book/en/v2/images/integration-manager.png

## Workflow Dictateur / Lieutenants. 

Ce workflow constitue une variante du workflow précédent. Il est particulièrement adapté au très gros projet ou aux projets réclamant une validation hiérarchique élevée. 

Il inclue un triple niveau avec 3 rôles : les développeurs, les lieutenants et le dictateur. 

![image](https://git-scm.com/book/en/v2/images/benevolent-dictator.png)

- Les développeurs poussent vers leur dépôt publique, ils travaillent chacun sur un sujet précis. 
  - Les développeurs poussent leurs modifications en utilisant un rebase du master (on verra que le master est géré par le dictateur). 
- Les lieutenants quant à eux sont responsables de l'intégration du travail des développeurs, ils ont une responsabilité au niveau d'une certaine partie du repository. Ils vont donc merger le travail des développeurs au niveau de leur propre master.
- Le dictateur va quant à lui merger le master de chaque lieutenant dans son propre master.
- Le dictateur va ensuite pousser depuis son propre master vers le master général, les développeurs vont pouvoir ensuite rebaser a partir du master général et relancer un cycle. 

## Notions avancées de workflow

Un guide existe en anglais qui vous permet de voir les workflows de manière exhaustive, ainsi que de savoir quand les utiliser. Vous pouvez vous y référer pour de plus amples détails : https://martinfowler.com/articles/branching-patterns.html


# Comprendre la contribution dans git

Plusieurs variables vont impacter votre façon de collaborer : 

- Le nombre de développeurs actifs sur le projet
- Le workflow sélectionné pour le projet
- Les accès en écriture (si vous pouvez écrire directement sur le master ou non)

Néanmoins nous allons voir comment créer une cohérence malgré l'ensemble de ces variables au travers de bonnes pratiques. 

## Les bonnes pratiques du commit. 

La première bonne pratique et la plus importante est de commiter à chaque entité logique. Si vous travaillez sur deux features distinctes par exemple n'essayez pas de committer conjointement les changements mais découpez votre commit en fonction de chaque entité logique. Cela simplifiera grandement les reverts en permettant de n'agir que sur une partie problématique si tous les autres élements sont quant à eux corrects. Ainsi si votre feature 2 est correcte mais que la 1 pose problème il sera beaucoup plus simple d'agir en cas de commits séparés. 

L'autre point à prendre compte est le message de commit qui doit décrire l'entité logique et les modifications qui lui ont été apportées de manière claire et concise. 

Le message se découpera en deux parties :
- Une description extrêmement brève (- de 50 caractères) qui détruit l'entité logique de manière globale.
- Une ligne blanche de séparation
- Une description plus en détail (si nécessaire) des changements effectués et de leur raison. 

Dernier point des bonnes pratiques avant d'effectuer le commit lancez la commande `git diff --check` qui vous permettra de vérifier qu'il n'y a pas d'erreur d'espacement. 

## Chronologie des workflows, un exemple de collaboration dans une petite équipe : 

Nous allons commenter le schéma suivant et comprendre la gestion chronologique dans le cadre d'une petite équipe avec un serveur centralisé :

![image](https://git-scm.com/book/en/v2/images/small-team-flow.png)

*Source : https://git-scm.com/book/en/v2/images/small-team-flow.png*

## Collaboration dans le cadre d'un projet publique (fork)

La collaboration dans le cadre d'un projet publique, notamment via des fork suit la logique suivante :

1) Création d'un clone du projet original
2) Creation d'une branche pour votre travail
3) Réalisation du travail sur cette branche avec emission de X commits
4) Création d'un fork écrivable (writeable) 
5) Ajout de ce fork comme remote au niveau de votre branche de travail
6) Push de cette branche de travail vers une branche acceuillant votre travail (et non sur le master pour permettre une sélection précise par le maintainer). 
7) Envoi d'une pull request vers le maintainer
   - La pull request peut avoir deux formes :
     - Utilisation de la commande git request-pull, et envoi du retour de cette commande par mail
     - Utilisation des fonctions built in sur github par exemple.
8) Merge de la part du maintainer dans le dossier canonique si requête acceptée sinon rejet.

## Maintien d'un projet 

