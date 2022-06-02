# Installation de Maven

Créez un dépôt git public nommé test-maven.

Clonez ce dépôt sur votre machine locale.

Installez Maven sur votre machine locale, puis lancez la commande suivante : `mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4`. Ceci va créer un projet maven simple. 

Committez ensuite ce projet. 

Rendez vous ensuite dans Jenkins, puis créez un projet test-maven-projet de type maven bien sûr. 

Nous allons maintenant procéder à la configuration, tout d'abord en renseignant la partie gestion de code source. Rappellez vous d'utiliser également vos crédentials qui ont été setup précédemment. 

![Capture d’écran de 2022-06-02 08-18-25](https://user-images.githubusercontent.com/98811386/171565568-fd874c39-49d3-4e46-9690-962256bc3694.png)
