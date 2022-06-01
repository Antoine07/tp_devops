# Pourquoi intégrer Github dans Jenkins ?

Les avantages sont les suivants : 

* Jenkins peut désormais une database de code directement dans son workspace local
* Github va pousser les changements vers jenkins qui à son tour va récupérer ce signal comme un déclenchement de build. C'est beaucoup moins intensif au niveau ressource que jenkins qui surveille constamment si github à des résultats. 
* Jenkins a désormais accès à des opérations sur github

# Configuration

Authentifiez-vous à votre compte github, puis en cliquant sur votre photo de profil allez dans settings, puis une fois dans settings sélectionner tout en bas "Developer settings".

Une fois arrivé dans cette section, sélectionner "Personal access token", puis new vous devriez arriver sur cet écran : 

![Capture d’écran de 2022-06-01 23-37-46](https://user-images.githubusercontent.com/98811386/171506406-10a3b2b3-13a3-4ee8-b700-0fd3f587e491.png)

Sélectionnez uniquement "public repo" dans scope pour l'instant, cliquez sur "gener(ate new token" puis gardez précieusement le token. 

Rendez-vous ensuite dans jenkins Administrer jenkins > Configurer le système. 

Scrollez ensuite jusqu'à la section github puis sélectionnez "add github server" :

![Capture d’écran de 2022-06-01 23-43-35](https://user-images.githubusercontent.com/98811386/171507121-5bab45c8-ad9b-4b9b-ba03-10890196887b.png)

Choisissez un nom puis cliquez sur ajouter dans credentials 

![Capture d’écran de 2022-06-01 23-46-14](https://user-images.githubusercontent.com/98811386/171507363-5d42a44d-858f-4aa2-823f-78ddf97d6016.png)

Remplissez le credentials en choisissant secret text dans le menu déroulant puis dans secret copiez le contenu de votre token, donnez un nom et enregistrez :

![Capture d’écran de 2022-06-01 23-48-06](https://user-images.githubusercontent.com/98811386/171507696-a2b4accd-983f-4059-b1c8-619231b67efe.png)

Finalement n'oubliez pas de sélectionner le nouveau credentials dans la page de configuration : 

![Capture d’écran de 2022-06-01 23-48-30](https://user-images.githubusercontent.com/98811386/171507776-dc6a5a42-e068-4bbb-a5f5-64d9c3426b22.png)


