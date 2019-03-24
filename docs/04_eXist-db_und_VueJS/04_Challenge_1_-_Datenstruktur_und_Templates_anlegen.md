# Challenge 1: Datenstruktur und Templates anlegen

Im [vorherigen Kapitel](../Erste_Schritte_mit_VueJS/00_Übersicht.md) haben Sie gelernt, wie man Variablen mit VueJS verwaltet und anzeigt.

**Zugehörige Beispieldatei**: `04_Challenge_1_-_Datenstruktur_und_Templates_anlegen.html`

## Aufgabe

Erstellen Sie das Datenmodell der Vue-Instanz und lassen Sie die Daten im HTML-Code an den passenden Stellen anzeigen. Nehmen Sie zuerst folgende JSON-Grußformel als Orientierungspunkt.

```json
{
  "quote":"Mit Verehrung Ihr ergebenster etc.",
  "edition":"Jean Paul – Sämtliche Briefe digital",
  "title":"An Friederike Christiane Elisabeth von Ompteda. Bayreuth, 24. Dezember 1819.",
  "url":"https://jeanpaul-edition.de/brief.html?num=VII_612",
  "language":"deu",
  "licence":null
}
```

## Lösungsansätze

* Öffnen Sie die Datei `04_Challenge_1.html` sowohl mit einem Editor und Browser.
* Wenn das Ergebnis im Browser wie vor den Änderungen aussieht, scheint Ihre Lösung richtig zu sein.
* Die zu bearbeitenden Stellen im Code sind mit `// TODO` oder `<!-- TODO -->` markiert.
* Erstellen Sie für jedes Element in der JSON-Grußformelvorlage eine neue `data`-Variable.
  * Benutzen Sie den Namen der Elements auch als Name für die Variablen
  * Übertragen Sie Werte für die Elemente per Hand in die Variable.
* Ersetzen Sie die hartgecodeten Informationen zur Grußformel im HTML-Bereich mit VueJS-Templates `{{ }}` an den passenden Stellen.
* Auch HTML-Attribute können VueJS-Variablen zugewiesen werden. Denken Sie dabei an ein Beispiel aus einer [vergangenen Challenge](../03_Erste_Schritte_mit_VueJS/10_Computed_Properties_-_Immer_auf_dem_aktuellsten_Stand.md) zurück:

```html
<button v-bind:disabled="!isValidNewItem">Hinzufügen</button>
```