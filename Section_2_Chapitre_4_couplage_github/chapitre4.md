# Pourquoi intégrer Github dans Jenkins ?

Les avantages sont les suivants : 

* Jenkins peut désormais une database de code directement dans son workspace local
* Github va pousser les changements vers jenkins qui à son tour va récupérer ce signal comme un déclenchement de build. C'est beaucoup moins intensif au niveau ressource que jenkins qui surveille constamment si github à des résultats. 
* Jenkins a désormais accès à des opérations sur github


