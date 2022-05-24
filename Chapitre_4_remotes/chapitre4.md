# Définition et utilité des dépôts "Remotes"

Jusqu'ici l'ensemble des fonctions que nous avons vues ont eu pour but de manager localement les changements. Vulgairement parlant nous nous sommes arrêtés aux commits. 

Cependant comme vu lors de l'introduction l'avantage d'un système DVCS réside surtout dans sa capacité à créer de la collaboration et coopération entre développeurs.

Pour que cette collaboration ait lieu, un prérequis essentiel est le fait que les dépôts soient accessibles à distance (que ce soit par internet ou tout autre réseau). 

Cet accès à distance est un prérequis pour deux éléments de la gestion de data collaborative. Les dépôts distants peuvent enregistrer de la data provenant de votre dépôt local (notion de push vers le dépôt distant), ou au contraire fournir de la data à votre dépôt local (notion de pull depuis le dépôt distant). 

Par simplicité et pour assimilation dans les explications suivantes nous utiliserons les notions de "pull" et "push" pour chacun de ces deux sens de communication. De même nous parlerons de "remotes" pour les dépôts distants. 

Le management de ces remotes repose sur la connaissance des actions suivantes :

* Ajout de remotes
* Suppression de remotes
* Management (et notion) de branches distantes

# Lister les remotes

La commande `git remote` sans modifieur, vous liste les remotes qui ont été configurés. 

Par exemple dans le cas d'un clone de dépôt le nom "origin" sera donné par défaut par git au dépôt depuis lequel vous avez clôné.

La commande `git remote` vous donne par défaut un raccourci qui correspond au nom (shortname) qui a été attribué à votre dépôt distant. 

Le modifieur `-v` vous permettra de connaître l'url attribuée par git à ce dépôt. 

Dernier point à noter, il peut exister de multiples remotes, notamment dans le cas où plusieurs collaborateurs considérés comme remotes. 

# Ajouter un remote

La commande `git remote add <shortname> <url>` permet d'ajouter manuellement un remote. 

`< shortname >` correspond au nom que vous souhaitez donner à votre remote.
`<url>` correspond bien entendu à l'url du git. 

L'utilisation du shortname vous permettra par la suite d'utiliser celui ci en place de l'url complète dans toutes les commandes liées à ce remote. 

> Imaginons que nous avons un remote dont l'auteur est votre formateur. en tappant la commande `git add formateur http://git/exemple` vous ajouterez le dépôt sous le short name "formateur". Si vous voulez récupérer les informations provenant de formateur vous n'aurez qu'à utiliser `git fetch formateur`. (Nous verrons plus avant la notion de fetch). 

# Récupérer de la data depuis les remotes (fetch et pull).

Pour récupérer de la data depuis un remote il faut utiliser la commande `git fetch <remote>`, où remote est le shortname précdemment vu. 

La commande git fetch va vous permettre de récupérer la donnée de toutes les branches du dépôt distant[^1]. 

Nous avons vu au chapitre précédemment que lors d'un clone, git crée automatiquement un remote "origin" donc `git fetch origin` récupérera toute la data de ce remote. 

Enfin si votre branche locale est configurée pour suivre une branche remote spécifique, vous pourrez utiliser la commande `git pull` afin de récupérer et merger cette branche distante vers votre branche locale[^1]. Une fois de plus dans le cadre d'un `git clone` votre branche master (ou tout autre nom de la branche de base) sera configurée automatiquement pour suivre la branche master du remote. 

# Pousser de la data (push)

Lorsque vous êtes satisfait de l'instantané sur lequel vous travaillez, vous pourrez pousser cet instantané vers le remote. Cette action est appelée "push" et se reflète dans la commande `git push <remote> <branch>`. Ainsi par exemple pour pousser vers "formateur" sur la branche "master" vous utiliserez la commande `git push formateur master`.

Attention cependant cette commande a plusieurs prérequis pour fonctionner : 

* Tout d'abord vous devez disposer des droits d'écritures sur le remote. En effet, un remote peut être en read only, ou en read / write. 
* Aucun autre instantané ne doit avoir été poussé sans que vous l'ayez fetché, pour éviter les conflits potentiels. 

# Inspecter un remote 

La commande `git remote show <remote>` vous permet d'obtenir des informations supplémentaires sur le remote que vous souhaitez inspecter. 

Cette commande est particulièrement utile lors d'utilisations complexes de git avec de multiples intervenants et des trackings multiples de branches. Nous ne la verrons pas en détail ici, puisqu'elle reprend majoritairement toutes les informations concernant les éléments vus précédemment. 

# Renommer et supprimer des remotes

La commande `git remote rename <SHORTNAME> <NEW SHORTNAME>` vous permet de modifier le raccourci local d'un remote. Par exemple vous pouvez renommer le remote "formateur" en "etudiant" via la commande `git remote rename formateur etudiant`

La commande `git remote remove <SHORTNAME>` permet d'effacer un remote, ainsi on pourra effacer le remote "etudiant" avec `git remote remove etudiant`. Un raccourci de la commande est `git remote rm <SHORTNAME>`.

[^1]: Nous verrons la notion de branches au chapitre suivant. 

# Tagging et Alias

Git supporte le tagging et les alias, ces notions n'étant pas essentiels à ce cours introductif, elles ne seront pas couvertes. 
