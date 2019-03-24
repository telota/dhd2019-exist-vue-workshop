# quoteSalute Datenstruktur

Dieser Abschnitt wiederholt einige Schritte und Inhalte, die Bereits im [Kapitel zur Nutzung von eXist-db](../02_XML_zu_JSON_in_eXist-db/00_Übersicht.md) behandelt wurden.

## XML-Daten

Eine Grußformel im quoteSalute ist in der eXist-db folgendermaßen hinterlegt:

```xml
<cit>
  <quote>Mit Verehrung Ihr ergebenster etc.</quote>
  <edition>Jean Paul – Sämtliche Briefe digital</edition>
  <title>An Friederike Christiane Elisabeth von Ompteda. Bayreuth, 24. Dezember 1819.</title>
  <url>https://jeanpaul-edition.de/brief.html?num=VII_612</url>
  <language>deu</language>
  <licence></licence>
</cit>
```

## Ergebnisse im Browser

Sie können sich ein zufälliges Zitat aus der eXist-db App von quoteSalute direkt über ihren Browser im Rohformat anzeigen lassen.

### Lokale eXist-db Instanz

* Eigene Datei `abfrage-challenge-02.xql` - [http://localhost:8080/exist/apps/quotesalute/abfrage-challenge-02.xql](http://localhost:8080/exist/apps/quotesalute/abfrage-challenge-02.xql)
* Vorgefertigte Datei `abfrage.xql` - [http://localhost:8080/exist/apps/quotesalute/abfrage.xql](http://localhost:8080/exist/apps/quotesalute/abfrage-challenge-02.xql)

### quoteSalute (live)

* Von quoteSalute bereitgestellte Schnittstelle - [https://correspsearch.net/quotesalute/abfrage.xql](https://correspsearch.net/quotesalute/abfrage.xql)

## JSON-Daten

Das Ergebnis wird letztendlich von der eXist-db App zu JSON serialisiert und zurückgeliefert.

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

Diese Grußformel wird fortan als Startbeispiel genutzt.