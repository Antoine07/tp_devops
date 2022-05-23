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

# Git Config

Lors de la première utilisation de git, un tool spécifique de git va nous permettre de le configurer plus finement. Cette étape n'est pas absolument nécessaire, elle peut être réalisée et ou modifiée à tout moment, néanmoins elle permet de maîtriser une configuration de base. 

La commande est la suivante : `git config`.




