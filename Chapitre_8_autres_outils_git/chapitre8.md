# Sélection de commits dans git

Il existe plusieurs moyens pour sélectionner des commits dans git :

- le sha1 de 40 caractères
- la sélection par les 4 premiers caractères (au minimum peut être plus) du sha1 (si il n'y a pas d'autres commits avec les mêmes 4 premiers caractères). 
- la sélection par le nom de la branche, dans le cas ou l'on met le nom de la branche à la place du sha1 alors on aura accès au dernier commit de cette branche. 
- Par l'utilisation du reflog, la commande `git reflog` permet d'accéder au reflog qui lui-même va indexer l'état de vos branches à un moment donné dans le temps. 
  - Vous pourrez ainsi utilisaer la syntaxe git show master@{yesterday} pour savoir l'état de votre master hier. 
  - Attention cependant le reflog est strictement local, et ne fonctionne que pour vos références locales. 
- Références d'ancêtres : en ajoutant un `^` à la fin d'une référence de commit vous pourrez voir son ancêtre, cad le commit précédent. Si l'on rajoute un numéro de cette façon `^2` on pourra voir les 2 parents (cas d'un merge), si l'on rajoute le tilde et un chiffre le nombre d'ancêtres constitués par le tilde. 

On peut également sélectionner des commits par "range" :

- la syntaxe en double points : elle permet de sélectionner une range de commits qui sont atteignables depuis une branche mais pas depuis un autre. 

> Considérons l'image suivante : 
>
> ![image](https://git-scm.com/book/en/v2/images/double-dot.png) 
>
> Si on utilise la syntaxe `git log master..experiment` on obtiendra D C comme retour, a savoir les logs sont non accessibles par master mais accessibles par experiment. 
>
> Cela vous permet de mapper vos commits et de savoir ce qui a été mergé ou non de manière plus facile.

- Des syntaxes tripartites existent également : `git log refA refB ^refC` va considérer tous les commits accessibles par refA ou refB mais pas par refC (une autre syntaxe est possible pour ce cas : `git log refA refB --not refC`)

- La syntaxe en `...` donne tous les commits accessibles par l'une ou l'autre des références mais non accessibles aux deux simultanément. On peut rajouter également `--left-right` pour rendre plus explicite le retour, cela permettra de savoir de quel cote est accessible le commit. Exemple 1 : `git log master...experiment` Exemple 2 : `git log --left-right master...experiment`
