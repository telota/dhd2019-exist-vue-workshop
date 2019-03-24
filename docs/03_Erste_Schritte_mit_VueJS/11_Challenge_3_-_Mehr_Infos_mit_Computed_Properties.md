# Challenge 3: Mehr Infos mit Computed Properties

**Zugehörige Beispieldatei**: `11_Challenge_3.html`

## Aufgaben

* Lassen Sie eine Information mit dem Text `Neuer Eintrag leer oder bereits vorhanden` einblenden, wenn `isValidNewItem` den Status `false` hat.
* Erstellen Sie ein neues Element im HTML-Bereich, wo Sie die Anzahl der Einträge in der Einkaufsliste anzeigen.
* Folgen Sie dabei den Lösungsansätzen und orientieren Sie sich am bereits existierenden Code.

## Lösungsansätze

* Die zu bearbeitenden Stellen im Code sind mit `// TODO` oder `<!-- TODO -->` markiert.
* Erstellen Sie im HTML-Bereich ein neues `<div>` oder `<span>`-Element und nutzen Sie die `v-if`-Direktive in Verbindung mit `isValidNewItem`. Mit einem `!` vor `isValidNewItem` können Sie die Werte `true` und `false` ins Gegenteil verkehren.
* Erstellen Sie im `computed`-Bereich eine neue Computed Property `numberOfItems`. Sie können sich die Anzahl aller Einträge in einer Liste z.B. folgendermaßen anzeigen lassen:

```js
let listOfAnimals = ['Hund', 'Katze', 'Maus'];
listOfAnimals.length; // 3
```

* Erstellen Sie im HTML-Bereich an der markierten Stelle ein neues Element und lassen dort die Anzahl der Listeneinträge anzeigen.
