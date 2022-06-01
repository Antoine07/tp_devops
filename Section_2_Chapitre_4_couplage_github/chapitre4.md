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

Vous pouvez maintenant tester votre connection. 

Il nous reste néanmoins de la configuration côté Jenkins et github. 

Il vous faudra maintenant créer une paire clé publique / privé pour vous connecter avec github afin que jenkins puissent pull les différents builds. Utiliser pour cela la commande `ssh-keygen -t rsa`.

Maintenant que nous disposons de cette paire de clé nous allons placer la clé publique dans github. On va se rendre à nouveau dans settings puis dans "SSH and GPG Keys" > new ssh key et on va copier le contenu de la clé publique puis enregistrer. 

On va maintenant cat la private key et l'intégrer dans jenkins. Administrer jenkins > Manage credentials

![Capture d’écran de 2022-06-02 00-02-35](https://user-images.githubusercontent.com/98811386/171509335-c36bba59-56b5-4007-8815-f4f55d24e07b.png)

On va sélectionner jenkins > identifiaux globaux > ajouter un identifiant. 

On va ensuite configurer comme suit en ajoutant notre private key : 

![Capture d’écran de 2022-06-02 00-05-29](https://user-images.githubusercontent.com/98811386/171509710-5fef0541-08cf-4293-aeab-b22960283fc1.png)


# Création d'un job test 

Nous allons maintenant créer un job de test pour voir si tout a bien fonctionner. Munissez vous de l'url d'un repo publique que vous possédez dans github, vous pouvez en créer un avec simplement un readme.md pour le test. Dans la section "Nouveau item" dans jenkins sélectionnez "projet freestyle".

Ensuite rendez vous dans la section Gestion de code source puis copiez l'url de votre répo git comme suit, n'oubliez pas de sélectionner votre credential : 

![Capture d’écran de 2022-06-02 00-13-53](https://user-images.githubusercontent.com/98811386/171510780-bd9cd186-8d13-43dd-87c5-dc3f854a951c.png)

Nous allons maintenant nous diriger vers la section Ce qui déclenche le build puis choisir l'option github hook trigger, analysons la section d'aide relative : 

![Capture d’écran de 2022-06-02 00-16-29](https://user-images.githubusercontent.com/98811386/171510942-36f5c14a-320a-4df3-90b4-7e2711535985.png)

Dernier point de cette configuration de job de test nous allons ajouter une action après le build et sélectionner "Set github status universal". Ensuite nous allons simplement choisir dans status result "One of default messages and statuses"

![Capture d’écran de 2022-06-02 00-20-11](https://user-images.githubusercontent.com/98811386/171511523-b0d9bdc8-97b0-4f5e-bd9e-f3298618d384.png)

