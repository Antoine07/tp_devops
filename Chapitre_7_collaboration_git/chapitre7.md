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

- Les développeurs poussent vers leur dépôt publique, ils travaillent chacun sur un sujet précis. 
- - deada
- Les lieutenants  


