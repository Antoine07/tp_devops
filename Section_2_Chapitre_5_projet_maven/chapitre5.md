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

Première constatation au niveau de la page globale des builds nous avons maintenant un graph indiquant que des erreurs se sont produites au niveau des tests :

![Capture d’écran de 2022-06-02 13-16-38](https://user-images.githubusercontent.com/98811386/171617921-9bf3c2e6-165e-4d64-a87f-666715ad3b9a.png)

On voit également que le build numéro 8 nous indique qu'il est en erreur avec une couleur warning : 

Si l'on s'intéresse plus en détail à ce build nous pouvons voir ce qu'il s'est passé : 

![Capture d’écran de 2022-06-02 13-18-50](https://user-images.githubusercontent.com/98811386/171618210-7baa0ca9-f76e-4c51-bdca-b671da17b88c.png)

Zoomons maintenant sur la partie test : 

![Capture d’écran de 2022-06-02 13-19-51](https://user-images.githubusercontent.com/98811386/171618361-a350faed-b78f-4f3b-9ab3-475706e08263.png)

Nous pouvons voir en détail où le test à échouer et quelle est la stack trace. 

Une autre vue est également disponible sur les tests spécifiquement : 

![Capture d’écran de 2022-06-02 13-22-46](https://user-images.githubusercontent.com/98811386/171618852-5875bb10-2b16-4bab-88d1-80c35e957277.png)

La console fournit également une vue chronologique des évènements : 

```html
Established TCP socket on 44365
<===[JENKINS REMOTING CAPACITY]===>channel started
Executing Maven:  -B -f /home/aurelien/.jenkins/workspace/test-projet-maven/maven-archetype-quickstart/pom.xml install
[INFO] Scanning for projects...
[INFO] 
[INFO] -------< org.apache.maven.archetypes:maven-archetype-quickstart >-------
[INFO] Building maven-archetype-quickstart 1.4
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:3.0.2:resources (default-resources) @ maven-archetype-quickstart ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /home/aurelien/.jenkins/workspace/test-projet-maven/maven-archetype-quickstart/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:compile (default-compile) @ maven-archetype-quickstart ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:3.0.2:testResources (default-testResources) @ maven-archetype-quickstart ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /home/aurelien/.jenkins/workspace/test-projet-maven/maven-archetype-quickstart/src/test/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.8.0:testCompile (default-testCompile) @ maven-archetype-quickstart ---
[INFO] Changes detected - recompiling the module!
[INFO] Compiling 1 source file to /home/aurelien/.jenkins/workspace/test-projet-maven/maven-archetype-quickstart/target/test-classes
[INFO] 
[INFO] --- maven-surefire-plugin:2.22.1:test (default-test) @ maven-archetype-quickstart ---
[INFO] 
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running App.AppTest
[ERROR] Tests run: 1, Failures: 1, Errors: 0, Skipped: 0, Time elapsed: 0.022 s <<< FAILURE! - in App.AppTest
[ERROR] shouldAnswerWithTrue(App.AppTest)  Time elapsed: 0.004 s  <<< FAILURE!
java.lang.AssertionError
	at App.AppTest.shouldAnswerWithTrue(AppTest.java:18)

[INFO] 
[INFO] Results:
[INFO] 
[ERROR] Failures: 
[ERROR]   AppTest.shouldAnswerWithTrue:18
[INFO] 
[ERROR] Tests run: 1, Failures: 1, Errors: 0, Skipped: 0
[INFO] 
[ERROR] There are test failures.

Please refer to /home/aurelien/.jenkins/workspace/test-projet-maven/maven-archetype-quickstart/target/surefire-reports for the individual test results.
Please refer to dump files (if any exist) [date].dump, [date]-jvmRun[N].dump and [date].dumpstream.
[JENKINS] Enregistrement des résultats des tests
[INFO] 
[INFO] --- maven-jar-plugin:3.0.2:jar (default-jar) @ maven-archetype-quickstart ---
[INFO] 
[INFO] --- maven-install-plugin:2.5.2:install (default-install) @ maven-archetype-quickstart ---
[INFO] Installing /home/aurelien/.jenkins/workspace/test-projet-maven/maven-archetype-quickstart/target/maven-archetype-quickstart-1.4.jar to /home/aurelien/.m2/repository/org/apache/maven/archetypes/maven-archetype-quickstart/1.4/maven-archetype-quickstart-1.4.jar
[INFO] Installing /home/aurelien/.jenkins/workspace/test-projet-maven/maven-archetype-quickstart/pom.xml to /home/aurelien/.m2/repository/org/apache/maven/archetypes/maven-archetype-quickstart/1.4/maven-archetype-quickstart-1.4.pom
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  2.690 s
[INFO] Finished at: 2022-06-02T13:08:12+02:00
[INFO] ------------------------------------------------------------------------
En attente que Jenkins finisse de récupérer les données

```
