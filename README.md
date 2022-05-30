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

### Chapitre 7 : Collaboration dans git

1) Workflows distribués VS centralisés 
2) Etude d'un système collaboratif réel
3) Contribution (fork, pull requests)
4) Maintien d'un projet (notion d'administration)

#### Collaboration avec github

1) Contribution à un projet
2) Maintien d'un projet 
3) Gérer un projet
4) Introduction au scripting de github (optionnel)

### Chapitre 7 : Panorama des autres outils de github

Révision, staging ...
(cette partie sera adaptée en fonction du temps jusqu'ici). 

### Chapitre 8 : Personnalisation de git 

1) Configuration
2) Attribus de git
3) La notion de hooks
4) Intégration de git dans les outils de développement (notamment visual studio code)

# Section 2 : Déploiement (avec jenkins)

### Introduction

1) Notion de déploiement utilité et contexte
2) Notion de développement continu

### Chapitre 1 : Installation de jenkins 

1) Review des différentes possibilités d'installation
2) Sélection d'une méthode d'installation

### Chapitre 2 : Utilisation de jenkins

1) Définition des builds
2) Actions sur les builds (creation, arrêt etc.)

### Chapitre 3 : Les pipelines Jenkins

1) Définition des pipelines
2) Définition et utilisation du jenkinsfile
3) Syntaxe et meilleurs pratiques

### Chapitre 4 : Gestion de jenkins

Configuration et gestion de jenkins

### Chapitre 5 : Sécurisation de jenkins

1) Contrôle des accès 
2) Gestion de la sécurité aspects généraux

### Chapitre 6 : Administration système de jenkins

1) Back up 
2) Monitoring

### Jenkins et architectures nécessitant du scaling

1) Architecture pour le scaling
2) Architecture pour le management

