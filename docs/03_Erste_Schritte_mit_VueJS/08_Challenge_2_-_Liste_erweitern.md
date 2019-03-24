# Challenge 2: Liste erweitern

Im [vergangenen Abschnitt](07_Vue_Methods_-_Funktionen_auf_Abruf.md) wurde gezeigt, wie man Funktionen auf Abruf in einer VueJS-Instanz nutzen kann. [Davor](06_Vue_Models_-_Daten_eingeben.md) wurde gezeigt, wie man Inputs mit dem VueJS Datenmodell koppelt.

**Zugehörige Beispieldatei**: `08_Challenge_2.html`

## Aufgabe

Kreieren Sie eine Möglichkeit neue Dinge zur Einkaufsliste hinzuzufügen. Folgen Sie dabei den Lösungsansätzen und orientieren Sie sich am bereits existierenden Code.

## Lösungsansätze

* Die zu bearbeitenden Stellen im Code sind mit `// TODO` oder `<!-- TODO -->` markiert.
* Schaffen eine neue `data`-Variable mit dem Namen `newItem`. Der Wert sollte leer sein (`''`). Vergessen Sie nicht Kommata zu setzen.
* Erstellen Sie im Methods-Bereich eine neue Funktion `addItem()`. Wenn diese ausgeführt wird, soll der aktuelle Wert von `newItem` in die `shoppingList` hinzugefügt werden. Nutzen Sie dazu die `push()`-Funktion für Listen (Beispiel siehe unten).
* Setzen Sie `this` richtig ein.
* Erstellen Sie im HTML-Bereich einen neuen Text-Input und binden Sie ihn über die `v-model`-Direktive an die entsprechende Variable.
* Erstellen Sie einen Neuen Button mit der Aufschrift "Hinzufügen".
* Wenn der Button geklickt wird, soll die Funktion `addItem` ausgeführt werden.

```js
let listOfAnimals = ['Hund', 'Katze', 'Maus'];
const panda = 'Panda';
listOfAnimals.push(panda); // ['Hund', 'Katze', 'Maus', 'Panda'];
```

## Besondere Herausforderung

* Wenn der "Hinzufügen"-Button geklickt wird, soll der `newItem`-Wert wieder geleert werden.
* Stellen Sie sicher, dass keine doppelten Einträge in die Einkaufsliste aufgenommen werden.
* Stellen Sie sicher, dass keine leeren Einträge in die Einkaufsliste aufgenommen werden.