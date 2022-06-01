# Méthodes d'installation

Il existe différentes méthodes d'installation pour jenkins, nous listerons ces méthodes avec la référence directe. Dans le cadre de ce cours nous allons utiliser docker, nous procédérons ensemble à l'installation d'un fichier war dont les prérequis sont les moins lourds. 

Vous trouverez ci-joint le lien vers la doc d'installation officielle pour chaque élément :

* Fichier War 
  * [WAR](https://www.jenkins.io/doc/book/installing/war-file/)
* Gestionnaires d'images :
  * [DOCKER](https://www.jenkins.io/doc/book/installing/docker/)
  * [KUBERNETES](https://www.jenkins.io/doc/book/installing/kubernetes/)
* OS : 
  * [LINUX](https://www.jenkins.io/doc/book/installing/linux/))
  * [MACOS](https://www.jenkins.io/doc/book/installing/macos/)
  * [WINDOWS](https://www.jenkins.io/doc/book/installing/windows/)
  * [AUTRES](https://www.jenkins.io/doc/book/installing/other/)
* Installation offline : 
  * [OFFLINE](https://www.jenkins.io/doc/book/installing/offline/)

# Procédure d'installation initiale

* Une fois le fichier war téléchargé vérifiez que vous avez java installé sur votre pc via la commande `java --version`
* Rendez-vous dans le dossier ou vous avez déposé le fichier jenkins.war, puis utilisez la commande `java -jar jenkins.war`
* Recopiez la clé qui vous est donné dans le script puis rendez vous sur http://localhost:8080 et entrez celle-ci à l'invite. Comme dans le screen suivant.

![Capture d’écran de 2022-06-01 22-01-50](https://user-images.githubusercontent.com/98811386/171491460-06f4b9b3-b91c-4f3d-b72e-8ea89f75b247.png)

* Cliquez ensuite sur installer les plugins suggérés :

![Capture d’écran de 2022-06-01 22-03-12](https://user-images.githubusercontent.com/98811386/171491740-e8b32f27-3e24-425b-a45c-40e24554c8e3.png)

* Après l'installation générer votre premier utilisateur : 

![Capture d’écran de 2022-06-01 22-07-18](https://user-images.githubusercontent.com/98811386/171492365-6ca8c11a-e5a1-42ba-b71d-90b27b0a4481.png)

* Puis personnalisez si vous le souhaitez l'url (dans le cadre de ce tutorial nous allons la laisser par défaut)
![Capture d’écran de 2022-06-01 22-07-39](https://user-images.githubusercontent.com/98811386/171492360-6b2ae609-159d-4280-a738-8997576581cb.png)

* Enfin vous êtes prêts à utiliser jenkins !

![Capture d’écran de 2022-06-01 22-07-49](https://user-images.githubusercontent.com/98811386/171492357-aede0ed1-c182-47c3-92a7-e17d5f296318.png)

