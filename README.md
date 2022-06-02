# Courses_git_deployment
Source pour le cours de git et déploiement.

# Section 1 : Git

### Chapitre 1 : Introduction

1) Définition d'un système de contrôle de versions
2) Local Version Control Systems vs Centralized Version Control Systems vs Distributed Version Control Systems
3) Historique de git
4) Différence de conception de git vs les autres CVS
5) Le fonctionnement en 3 états de git (modified, staged, committed)

### Chapitre 2 : Set up 

1) Installation de git 
2) Ligne de commande vs GUI 
3) Configuration initiale de git
4) Les commandes d'aide de git

### Chapitre 3 : Les basiques de git

1) Initialisation ou récupération d'un repository
2) Effectuer des changements dans un dépôt git
3) Comprendre l'historique des commits
4) Gérer le retour en arrière dans git

### Chapitre 4 : Les remotes

1) Définition et utilité des dépôts "remotes"
2) Lister les remotes
3) Ajouter un remote
4) Récupérer de la data depuis les remotes (fetch et pull) 
5) Inspecter un remote 
6) Renommer et supprimer des remotes
7) Tagging et Alias

### Chapitre 5 : Le système de branches de git 

1) Introduction à la notion de branches
2) Conception de git et impact sur les branches dans git
3) Commandes de base sur le branching, le merging et leur gestion
4) Logiques de gestion des branches
5) Interaction des branches locales et distantes
6) Merge VS Rebasing

### Chapitre 6 : Git côté serveur

1) Particularités de git côté serveur
2) Implémentation d'un bare repository sur un serveur

### Chapitre 7 : Collaboration dans git (et github)

1) Workflows distribués VS centralisés 
2) Comprendre la contribution dans git
3) Collaboration dans le cadre d'un projet publique (fork)
4) TP : Structuration d'un git pour une nouvelle société.

### Chapitre 8 : Panorama des autres outils de git

1) Sélection de commits dans git
2) Staging interactif
3) Stashing
4) Git clean
5) Git grep
6) Recherche dans les logs
7) Travail de l'historique des commits
8) Filter-branch
9) Git Reset et Git Checkout
10) La fonctionnalité `git rerere`

# Section 2 : Déploiement (avec jenkins)

### Introduction

1) Définition du déploiement (d'applications / sites)
2) Jenkins, rôles buts et fonctionnement théorique

### Chapitre 1 : Installation de jenkins 

1) Méthodes d'installation
2) Configuration initiale

### Chapitre 2 : Interface de jenkins

1) Aperçu de l'interface

### Chapitre 3 : Couplage avec github

1) Pourquoi intégrer github dans jenkins ? 
2) Configuration
3) Création d'un job test

### Chapitre 4 : Installation du plugin Maven

1) Pourquoi Maven ? 
2) Installation du plugin Maven
3) Construction du premier projet Maven

1) Installation de Maven
2) Configuration du projet dans Jenkins

