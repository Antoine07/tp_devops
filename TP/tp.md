# TP : Intégration et développement continu

## Objectif

L'objectif de ce tp est de partir d'une stack connue "React" et d'intégrer progressivement les éléments fonctionnels de l'application, puis d'automatiquement déployer ces éléments via jenkins. 

Git sera donc responsable du système de branching, mais aussi de l'intégration continue. La stratégie sélectionné sera celle d'un intégration manager (stratégie abordée en section 2 chapitre 7 pour rappel).

Jenkins sera donc responsable du build vers un dossier local qui sera la simulation de votre dossier de production. 

Nous nous baserons sur le tutoriel de React pour simuler les améliorations de code. Ce tutoriel est en fonction, ce qui n'est pas la meilleure pratique actuelle, mais cela ne rentre pas en compte dans l'immédiat. Vous trouverez l'ensemble du tutoriel à cet url : https://react.dev/learn/tutorial-tic-tac-toe. Dans ce tutoriel nous suivrons l'installation locale selon les étapes décrites ci après. 

Le tp se divisera en plusieurs étapes qui doivent être accomplie séquentiellement. 

## Etape 1 : Set up des repositories

Dans cette étape vous devrez : 
* Set up un "blessed repository"
* Set up un "developer public repository"
* Set up un "developer private repository"
* Documenter les relations entre chacun des repositories et les stakeholders : "Integration manager" et "Developper(s)". 
> * Qui a la responsabilité de quelles actions (pull, push, merge request) ? 
> * Quand un nouveau développeur arrive quelles sont les méthodes et étapes appliquées ?

La première version du blessed repository doit contenir l'initialisation d'un nouveau projet react. Dans l'immédiat aucune modification sur ce projet vide n'est à apporter.

## Etape 2 : Définition des méthodes de gestion des branches de developpement long de features, correction de bugs et règles de commits

Dans cette étape vous devrez documenter :
* La stratégie de création des branches et vérifier que celle-ci produit une intégration continue fiable, vous pourrez vous fonder sur la partie "Logiques de gestion des branches" du chapitre 5 "branches". 

## Etape 3 : Ajout de la première fonctionnalité display d'une X partie 1

Notre première feature sera symbolisée par la version extrêmement minimale du tictactoe que nous allons produire sous la forme d'une display d'une croix par la fonction suivante. 

Dans cette partie nous avons pour but uniquement de refléter dans le code source le travail d'un développeur qui aurait produit la fonction suivante : 

```js
export default function Square() {
  return <button className="square">X</button>;
}
```

Le développeur devra publier la modification, et l'integration manager la valider selon les règles mises en place précédemment. 

## Etape 4 : Ajout de la première fonctionnalité display d'une X partie 2 

Assurez vous de disposer localement d'une installation de jenkins. 

Dans cette étape vous devrez : 
* Produire le pipeline nécessaire dans git pour que jenkins puisse automatiquement déployer l'application lors de la mise à jour du blessed repository par l'integration manager. Le résultat attendu est que les fichiers produits par le build soit insérer dans un dossier "production"
* Vous assurez du retour en cas de déploiement correcte dans git. 
* Prévoir les étapes de test que vous souhaiterez effectuer dans la partie CD (le coding de ces étapes n'est pas nécessaire si les deux éléments précédents sont remplis)

## Etape 5 : build du board 

Dans cette étape vous devrez intégrer le code suivant en vous assurant que la démarche des étapes 3 et 4 est suivie et respectée : 

```js 
export default function Board() {
  return (
    <>
      <div className="board-row">
        <button className="square">1</button>
        <button className="square">2</button>
        <button className="square">3</button>
      </div>
      <div className="board-row">
        <button className="square">4</button>
        <button className="square">5</button>
        <button className="square">6</button>
      </div>
      <div className="board-row">
        <button className="square">7</button>
        <button className="square">8</button>
        <button className="square">9</button>
      </div>
    </>
  );
}
```

## Etape 6 : Correction d'un bug 

Dans cette étape vous allez tout d'abord, en respectant le cycle des étapes 3 et 4 : 

* Intégrer la fonction square : 

```js

function Square() {
  return <button className="square">1</button>;
}

```

* Ensuite updater le board component : 

```js 
export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
      <div className="board-row">
        <Square />
        <Square />
        <Square />
      </div>
    </>
  );
}
```

* Modifier la fonction square de la façon suivante : 

```js
function Square({ value }) {
  return <button className="square">value</button>;
}
```

* Déployer le code en production. 

* Enfin corriger le bug. Pour cette partie vous devrez utiliser les branches adéquates ainsi que les méthodes de révision adequate. Documentez ce que vous avez produit pour résoudre ce bug grâce à la mise en place de la mise à jour suivante : 

```js
export default function Board() {
  return (
    <>
      <div className="board-row">
        <Square value="1" />
        <Square value="2" />
        <Square value="3" />
      </div>
      <div className="board-row">
        <Square value="4" />
        <Square value="5" />
        <Square value="6" />
      </div>
      <div className="board-row">
        <Square value="7" />
        <Square value="8" />
        <Square value="9" />
      </div>
    </>
  );
}
```

## Dernière étape :

* Reprenez le tutoriel de tictactoe react. 
* Construisez maintenant toutes les étapes qui vont vous permettre d'ajouter progressivement toutes les fonctionnalités jusqu'au jeu final.
* Documentez les étapes de validation pour chaque stakeholder (developer, integration manager) sur git
* Documentez l'ensemble des builds produits vers la production

Fournissez pour la correction les gits ainsi que l'historique des builds locaux et le dossier "production" final.