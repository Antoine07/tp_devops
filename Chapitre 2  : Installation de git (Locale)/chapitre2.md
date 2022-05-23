# Installation de git (locale)

## Installation sur linux :

L'installation sur linux se fait via les gestionnaires de packets :

* `sudo dnf install git-all` pour fédora et associés
* `sudo apt install git-all` pour débian et associés (dont ubuntu)

## Installation sur MacOs :

* Vous pouvez dans un terminal tapper la ligne de commande suivante : `git --version`. Si git n'est pas déjà installé il vous proposera de s'installer (notamment via Xcode).
* Si vous voulez une version plus récente un binaire d'installation est maintenu [ici](https://git-scm.com/download/mac)

## Installation sous windows : 

* Un build officiel est disponible à l'adresse suivante : [https://git-scm.com/download/win](https://git-scm.com/download/win)
* Une installation automatique est disponible via [Chocolatey](https://chocolatey.org/packages/git), ce package est maintenu par la communauté.

## Installation depuis la source :

Il est possible d'installer git depuis la source elle-même pour avoir la version la plus récente. Cette installation n'est pas couverte dans ce cours, car non nécessaire à son bon suivi et plus chronophage. 
Si néanmoins vous en avez besoin pour un projet, l'installation est expliquée en détail ici : [https://git-scm.com/book/en/v2/Getting-Started-Installing-Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

> TP 1 : Installer Git. 

# Ligne de commande et interface GUI

Lors de ce cours nous allons utiliser uniquement la ligne de commande qui permet de gérer git entièrement. Néanmoins il est capital que vous sachiez que certains systèmes GUI vous permettent de gérer git. Néanmoins nous n'en sélectionnerons pas un dans ce cours afin d'avoir une connaissance maximale de git. 

# Git Config

Lors de la première utilisation de git, un tool spécifique de git va nous permettre de le configurer plus finement. Cette configuration peut-être revue à tout moment. 

La commande est la suivante : `git config`.

Git config va stocker les éléments de configuration sur 3 niveaux : 

1) `[path]/etc/gitconfig` => définit les valeurs communes à tous les utilisateurs et tous les repositories.
2) `~/.gitconfig` ou `~/.config/git/config` => valeur spécifique à un utilisateur donné, agit sur tous les repositories que vous allez utiliser en tant qu'utilisateur. Il est possible de les lire ou écrire en passant l'option `--global`
3) `config` dans `.git/config` à l'intérieur du repository dans lequel vous travaillez. 

Chaque fichier d'un niveau inférieur est écrasé par celui d'un niveau supérieur. La commande `git config --list --show-origin` permet de voir chaque réglage et son origine.

## Les réglages d'identité

Lors d'une nouvelle installation de git la première chose à faire est de définir votre identité. Cette dernière sera utilisée dans les commits afin d'en savoir l'auteur. Si vous passez l'option `--global` vous n'aurez à le faire qu'une fois. 

Vous devez régler votre username et votre email : 

> `git config --global user.name "John Doe"`
 
> `git config --global user.email johndoe@example.com`

Si vous devez utiliser une autre identité pour un projet specifique il suffira de faire appel à cette commande dans le repository de ce projet sans l'option `--global`







