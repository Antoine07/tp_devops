# Jenkins controller et jenkins agent node

Le problème géré par les jenkins controller et les agents revêt plusieurs formes : 

- Lorsque les teams grandissent les besoins de scaler Jenkins s'accentuent
- Les équipes de développement peuvent avoir besoins de tester sur de multiples plateformes (windows, mac, unix, iOs, Android ...)
- Une seule instance de jenkins n'est pas suffisante pour relever ces défis. 

La solution concernant jenkins provient de l'utilisation des agents, le schéma suivant montre l'organisation de jenkins autour de ce concept : 

![Capture d’écran de 2022-06-02 22-47-03](https://user-images.githubusercontent.com/98811386/171735270-a08d93e8-0cc2-4bf1-b983-b52ba7f1e278.png)
*Source : https://www.youtube.com/watch?v=nCKxl7Q_20I*

Les agents jenkins sont des éléments déportés capables de réaliser les tâches demandés par jenkins. Ils répondent particulièrement au double problème posé en permettant à la fois le scaling mais aussi le fait que chaque agent peut être sur un OS différent. 

Dans le cas où il existe un jenkins controller node et de multiples agents, le controller node est l'instance jenkins que nous avons déjà installée. Une fois les agents installés ils vont gérer sous la direction du controller node les tâches concrètes qui leur sont confiées. 

# Configuration

La communication entre jenkins et ses agents passe par l'émission d'un système de clés publiques / privées. 

La clé privée sera contenue du côté de jenkins et la clé publique du côté de l'agent (on stockera cette clé privée dans les crédentials globaux de jenkins comme nous l'avons fait pour la clé privée de git). 

Du côté de la machine qui sera l'agent il faudra donc ajouter la clé publique comme clé autorisée (authorizedkeys dans le dossier ssh en général). 

Ensuite il faudra se rendre sur l'instance jenkins puis dans Administrer Jenkins > Gérer les noeuds. 

Vous devrez donc vous retrouver en face de l'écran suivant : 

![Capture d’écran de 2022-06-02 22-57-49](https://user-images.githubusercontent.com/98811386/171737074-b56d2411-8abd-4d86-8827-bc7421e3a7f3.png)

La machine maître étant la ou l'instance jenkins est configurée. 

Nous allons maintenant ajouter un node. 

Le premier step de la configuration d'un nouveau noeud est le suivant : 

![Capture d’écran de 2022-06-02 23-00-04](https://user-images.githubusercontent.com/98811386/171737475-c2391aab-242c-438f-b1f2-f4c8bc5ad099.png)

Nous allons choisir un nom explicite puis également cocher l'aspect permanent de l'agent (dans ce cas nous considérons que la machine est dédiée à être un agent). 

![Capture d’écran de 2022-06-02 23-01-30](https://user-images.githubusercontent.com/98811386/171737629-d9274ace-2c24-470f-bc03-e54ad7a942f5.png)

Nous sommes désormais au deuxième step de la configuration et nous allons avoir à faire plus de choix. 

Premier point nous remarquons que nous pouvons choisir un nombre d'executeurs exactement comme nous le pouvons pour notre instance principale. Les exécuteurs sont le nombre d'instance simultanée qui peuvent chacune gérer un job en parallèle. 

Le remote root directory sera le répertoire dans lequel jenkins va stocker tous les éléments nécessaires à son caching et aux builds.

Les labels sont des éléments de définition de l'agent. Ils permettent de définir les labels relatifs aux agents qui eux-mêmes définissent ce que peut faire l'agent. Dans notre cas par exemple nous pourrions déterminer le label "linux" pour l'opposer à "windows" ou "macos". La partie utilisation vient compléter ce label, on peut demander au noeud d'être utilisé autant que possible ou seulement pour les labels qui lui correspondent. 

Les méthodes de lancement sont également importantes. Comme nous avons configuré jenkins pour fonctionner par ssh nous allons utiliser cette option. La première option requiert que le jar d'agent jenkins soit installé sur le système de l'agent. 

La disponibilité permet de définir la méthode de mise a disposition de l'agent que vous souhaitez. Particulièrement utile si vous êtes sur une infrastructure cloud et souhaitez réduire vos coûts. 

Une fois cette configuration accomplie vous disposez d'un agent !

# Attribution des tâches

Pour exécuter une tâche spécifiquement sur cet agent vous aurez accès à une nouvelle configuration dans les jobs vous permettant de restreindre l'accessibilité de la tâche à certains labels. Cela vous permettra par exemple de distribuer les tâches entre un environnement linux ou windows. 
