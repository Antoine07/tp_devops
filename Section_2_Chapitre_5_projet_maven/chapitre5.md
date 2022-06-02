# Installation de Maven

Créez un dépôt git public nommé test-maven.

Clonez ce dépôt sur votre machine locale.

Installez Maven sur votre machine locale, puis lancez la commande suivante : `mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4`. Ceci va créer un projet maven simple. 

Committez ensuite ce projet. 

# Configuration du projet dans Jenkins

Rendez vous ensuite dans Jenkins, puis créez un projet test-maven-projet de type maven bien sûr. 

Nous allons maintenant procéder à la configuration, tout d'abord en renseignant la partie gestion de code source. Rappellez vous d'utiliser également vos crédentials qui ont été setup précédemment. 

![Capture d’écran de 2022-06-02 08-18-25](https://user-images.githubusercontent.com/98811386/171565568-fd874c39-49d3-4e46-9690-962256bc3694.png)

Configurez ensuite les triggers, comme nous l'avons déjà vu en raison de l'utilisation de jenkins en local nous utilisons une scrutation périodique, mais cette pratique est à éviter et on préférera les hooks poussées par github : 

![Capture d’écran de 2022-06-02 08-25-36](https://user-images.githubusercontent.com/98811386/171566783-38ba080b-0b6b-4c5b-92bf-a59c7a3db99d.png)

Il reste maintenant à définir la localisation du fichier pom.xml ainsi que l'objectif à suivre : 

![Capture d’écran de 2022-06-02 08-29-36](https://user-images.githubusercontent.com/98811386/171567341-b5a81a34-e897-44f9-ba44-206696f97587.png)

# Lecture du build et de la logique sous-jacente. 

Nous allons maintenant procéder à un build, et faire sa lecture : 

![Capture d’écran de 2022-06-02 13-08-44](https://user-images.githubusercontent.com/98811386/171616697-4c5967cd-df33-429c-b813-9f517bda0e2b.png)

A ce niveau nous avons plusieurs niveaux d'informations, tout d'abord le build s'est déroulé sans problème et on a un retour du check, on peut aussi voir que les tests ont été passés sans soucis. 

Nous allons maintenant modifier la classe test qui se trouve dans src/test/java/App/Apptest.java:

```java
public class AppTest 
{
    /**
     * Rigorous Test :-)
     */
    @Test
    public void shouldAnswerWithTrue()
    {
        assertTrue( false );
    }
}
```

