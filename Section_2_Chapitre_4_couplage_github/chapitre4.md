# Pourquoi intégrer Github dans Jenkins ?

Les avantages sont les suivants : 

* Jenkins peut désormais une database de code directement dans son workspace local
* Github va pousser les changements vers jenkins qui à son tour va récupérer ce signal comme un déclenchement de build. C'est beaucoup moins intensif au niveau ressource que jenkins qui surveille constamment si github à des résultats. 
* Jenkins a désormais accès à des opérations sur github

# Configuration du côté de github.

Authentifiez-vous à votre compte github, puis en cliquant sur votre photo de profil allez dans settings, puis une fois dans settings sélectionner tout en bas "Developer settings".

Une fois arrivé dans cette section, sélectionner "Personal access token", puis new vous devriez arriver sur cet écran : 


![Capture d’écran de 2022-06-01 23-37-46](https://user-images.githubusercontent.com/98811386/171506406-10a3b2b3-13a3-4ee8-b700-0fd3f587e491.png)
