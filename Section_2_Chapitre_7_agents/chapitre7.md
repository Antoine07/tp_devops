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



