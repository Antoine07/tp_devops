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

[^1]: Nous verrons la notion de branches au chapitre suivant. 
