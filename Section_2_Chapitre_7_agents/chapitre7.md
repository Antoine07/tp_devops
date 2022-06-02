# Jenkins controller et jenkins agent node

Le problème géré par les jenkins controller et les agents revêt plusieurs formes : 

- Lorsque les teams grandissent les besoins de scaler Jenkins s'accentuent
- Les équipes de développement peuvent avoir besoins de tester sur de multiples plateformes (windows, mac, unix, iOs, Android ...)
- Une seule instance de jenkins n'est pas suffisante pour relever ces défis. 

La solution concernant jenkins provient de l'utilisation des agents, le schéma suivant montre l'organisation de jenkins autour de ce concept : 



![Capture d’écran de 2022-06-02 22-47-03](https://user-images.githubusercontent.com/98811386/171735270-a08d93e8-0cc2-4bf1-b983-b52ba7f1e278.png)
