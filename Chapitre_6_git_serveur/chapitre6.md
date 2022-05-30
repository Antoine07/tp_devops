# Particularitès de git côté serveur 

## Particularité et utilité d'un répertoire git sur un serveur. 

La conception de git, rend l'utilisation d'un répertoire tierce servant à la communication "naturelle". En effet, bien que vous disposiez d'un miroir sur chacune des machines des collaborateurs et qu'une communication directe est possible ceci est fortement découragé car réducteur au niveau des possibilités offertes par git. 

La méthode la plus logique est de disposer d'un répertoire "neutre" ou plutôt tierce vers lequel chacun des collaborateurs va pusher et puller de l'information. Ceci permet une organisation plus logique et une meilleure classification des différents rôles. 

Un "remote repository" sera souvent qualifié de "bare repository". Ce qu'il faut comprendre par là est qu'il ne disposera pas d'un working repository puisqu'il n'y a pas de vocation pour ce répertoire à modifier le code directement. Il servira de relais d'informations et ne conservera donc que les éléments constituant le dossier .git. 

Avant de procéder à l'installation d'un serveur git plusieurs options se présentent à vous, elles sont relatives aux choix que vous devez faire : 

- Décider si l'utilisation d'un serveur git sur un serveur qui vous est propre est utile ou non. Dans le cas ou cela ne serait pas un prérequis vous pourrez vous reposer sur des solutions déjà présentes permettant d'avoir un compte hosté et de gérer ces dépôts à distance. 
- Sélectionner les protocoles qui correspondent le mieux à vos besoins avec leurs pours et leurs contres (que nous allons voir immédiatement). 

## Les 4 protocoles de git. 

### Local Protocol

Ce protocole comme son nom l'indique consiste à disposer d'un remote repository dans un autre repertoire du même host (on évitera cependant que ce host soit un même ordinateur physique et on préférera des systèmes de type NFS, en tout cas un système de fichiers partagés). 

Les actions relatives à ce protocole peuvent être effectuées de deux façons, les deux utilisant le chemin "path" vers le local repository : 

- `git clone /srv/git/project.git`
- `git clone file:///srv/git/project.git`

La différence entre ces deux syntaxes réside dans le fait que lorsque `file://` est utlisé git utilise le système de gestion de transfert de data via un network. Utiliser un path classique est toujours plus rapide, mais vous pourrez avoir à utiliser `file://` notamment lors de migration d'anciens systèmes de VCS vers git. Vous pouvez utiliser de manière classique toutes les fonctionnalités de git faisant appel à un URL. 

Ce protocole a plusieurs avantages :

- Si l'on dispose déjà d'un système de gestions de fichiers partagés le set up est simple rapide, et réutilise la gestion des droits READ/WRITE de ce système. 
- Il permet une collaboration extrêmement rapide en pushant / pullant sur un élément local et en se dispensant de certaines étapes d'un remote repository.

Il a également quelques défauts majeurs : 

- Un système de gestion de fichiers est généralement plus difficilement accessible depuis n'importe quel réseau, il requiert une gestion des utilisateurs et de leur authentification. 
- L'accès rapide à la data n'est un avantage que si le système de gestion de fichiers est lui-même rapide, il peut parfois être beaucoup plus lent suivant la configuration. 
- La sécurité et l'intégrité sont moindres. Chaque utilisateur peut accéder au remote directory de manière directe et corrompre les fichiers.  

### Les protocoles HTTP

Il existe deux protocoles http, qualifiés de "dumb HTTP" et "smart HTTP". Le protocol smart http a été introduit dans git 1.6.6.

#### Smart HTTP 

Il agit de manière très similaire à un protocole de type SSH ou Git, mais utilise les ports HTTPS et supportent une multitude d'authentification des protocoles http (username et password par exemple). 

Il introduit la possibilité de lire la data lors des pulls de manière libre puis de demander une authentification pour les pushs. Tout cela est fait sur la même url. C'est l'un des services les plus populaires pour sa facilité d'utilisation, et sur github par exemple l'url du dépôt est la même que celle utilisée pour les clones et les pushs si les droits sont accordés. (Récemment des restrictions de sécurité ont été mises en place et demandent maintenant une authentification SSH pour l'utilisation de github). 

#### Dumb HTTP 

Nous passerons rapidement sur ce protocole maintenant ancien et peu utilisé. Il faut juste savoir que cette possibilité existe et est très facile : il permet de délivrer par http les fichiers "raws" de git et réclame une hook post update.

Les protocoles http, surtout le smart http dispose des avantages suivants : 

- Le protocole est simple (ne comporte qu'une seul url pour toutes les actions) et autorise des authentifications plus simples que des clés SSH.
- Il est rapide.
- Le protocole HTTPS est utilisable permettant l'encryption des données transférées et également une communication facile malgré les firewalls qui acceptent la plupart des requêtes https.

Mais ils ont également les défauts suivants : 

- La gestion des authentifications peuvent être ennuyeuses puisque les credentials sont redemandés à chaque connection les nécessitant. 

### Le protocole SSH

Le protocole SSH est largement employé pour différentes actions techniques dans la plupart des entreprises, et si il n'est pas employé il est facilement déployable. 

L'accès à un ssh via git peut se faire de deux façons : 

- `git clone ssh://[user@]server/project.git`
- `git clone [user@]server:project.git`

Dans les deux cas en cas d'absence de précision du username git va supposer qu'il s'agit du username préréglé dans ses propres paramètres.

Les avantages du SSH sont liés à l'utilité même de ce protocole : 

- Large utilisation dans les entreprises et configurations déjà réalisées dans la plupart des cas
- Sécurité (encryption et authentification)
- Compactage de la data avant son transfert

Les contres : 

- Même pour un accès en lecture le protocole SSH requiert une authentification, ce qui rend votre git moins largement diffusable notamment pour les projets open sources.
- Ceci n'est un inconvénient que si vous comptez utiliser git en dehors d'un cadre strictement corporate. 

### Le protocole git 

Le protocole git est un daemon qui tourne sur le port 9418 par défaut. Il est très similaire au protocole SSH, mais fonctionne sans aucune authentification. Il s'agit donc généralement de repository mis en place en lecture seule, dans lequel le push n'est pas autorisé (en raison de l'absence d'authentification). 

Pour permettre l'accès en read only vous devez créer un fichier `git-daemon-export-ok` le daemon ne servira le repository que si ce fichier est présent. 

Les avantages : 

- Souvent le protocole qui sert de la manière la plus rapide par un network, en utilisant les mêmes protocoles que le SSH pour le transfert de données mais sans l'encryption. 

Les inconvénients : 

- Ce protocole est utilisé pour la diffusion large en read only, mais généralement il doit être pairé avec un protocole de type SSH pour les quelques développeurs qui vont pusher vers ce repository du fait du manque d'authentification.
- Le protocole est plus dur à setuper du fait de l'utilisation de son propre daemon et requiert xinetd ou ssytemd configuration ...
- Il requiert également l'accès au port 9418 qui peut être problématique pour certains firewalls. .

# Implémentation d'un bare repository sur un serveur.

## Création d'un bare repository.

Comme nous l'avons vu dans la partie précédente, pour qu'un git soit exporté vers un serveur il faut d'abord faire de notre repository un "bare repository". 

Pour cela l'option --bare d'un git clone va permettre de créer un bare repository. Une convention consiste à nommer le bare repository avec le suffixe .git. La commande git clone va alors opérer avec les modificateurs suivants

- `git clone --bare <NOM DU PROJET> <NOM DU PROJET .git>`

Cette commande va créer un nouveau git repository de type bare dans le directory <NOM DU PROJET .git> par exemple myproject.git en tant que répertoire. 
  
## Placer le bare repository sur un serveur. 

Le dépôt d'un bare repository peut être effectuer de manière classique sur un serveur (scp etc.)
  
Les impacts sont les suivants : 
  
* Toute personne ayant accès à la localisation du bare repository en read only peut désormais utiliser les fonctionnalités de cloning et de pull du bare repository. 
* Toute personne disposant d'un accès ssh en write disposera également automatiquement des fonctionnalités de push. 
* Dernier point à noter, si à ce stade vous effectuez la commande suivante : `git init --shared` sur le serveur, vous créerez les droits d'écriture de groupe dans ce repository. Cela ne détruira pas toute action antérieure comme les commits etc.
  
Nous avons vu un setup complet d'un remote repository, si vous souhaitez ajouter de nouveaux utilisateurs, il ne restera alors qu'à rajouter des comptes SSH.
  

## Clés SSH et git 

Dans le cadre d'une gestion d'un nombre restreint de collaborateurs la gestion de git se fera donc par l'ajout de clés SSH. On ne rentrera pas dans le détail dans ce cours. 
Pour plus de détails vous pouvez vous reporter aux chapitres suivants :  

  * https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key
  * https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server
  
> Note nous ne couvrirons pas dans ce cours les autres protocoles en détails, en cas d'utilisation des autres protocoles vous disposez de chapitre dédié dans le livre référence. 

