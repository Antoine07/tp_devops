# Git Serveur

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

- git clone /srv/git/project.git
- git clone file:///srv/git/project.git
