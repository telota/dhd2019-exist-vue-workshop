# Challenge 2: Neue Grußformel auf Knopfdruck

**Zugehörige Beispieldatei**: `10_Challenge_3.html`

## Aufgabe

Statt immer die Seite neu Laden zu müssen, soll eine neue Grußformel auf Knopfdruck geholt werden.

## Vorgehensweise

* Öffnen Sie die Datei `08_Challenge_8.html` sowohl mit einem Editor und Browser.
* Wenn das Ergebnis bei jedem Druck auf den neuen Knopf anders aussieht, scheint Ihr Ergebnis richtig zu sein.
* Die zu bearbeitenden Stellen im Code sind mit `// TODO` und `<!-- TODO --> markiert.
* Legen Sie den `methods`-Bereich der VueJS-Instanz an
* Erstellen Sie eine Funktion `fetchSalute()` und nutzen Sie den Code aus der `created()`-Methode nach.
* Erstellen Sie im HTML-Bereich an der markierten Stelle einen Button mit der Aufschrit `Neu` und verbinden Sie ihn mit der `fetchSalute()`-Funktion über `v-on:click`.

## Bonusaufgabe

Verkürzen Sie den Inhalt der `created()`-Methode. Brauch man den Code wirklich zwei Mal?