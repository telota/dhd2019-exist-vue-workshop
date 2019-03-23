# Challenge 1: Eine Grußformel abrufen

## Aufgabe

Versuchen Sie die Datenbankabfrage in der Datei `abfrage-challenge-01.xql` so zu manipulieren, dass nur noch eine einzige Grußformel (die erste) zurückgeliefert wird.

## Gegeben

* `abfrage-challenge-01.xql`
* Die Datei ist schon so manipuliert, dass nur der 3. Treffer aus einer Trefferkollektion zurückgegeben wird.

```xquery
xquery version "3.0";

(: Deklaration von Namensräumen. Wichtig für die Arbeit mit TEI-XML-Daten :)
declare namespace tei="http://www.tei-c.org/ns/1.0";

(: Variable zum Speichern des Daten-Verzeichnispfads :)
let $data := "/db/apps/quotesalute/data"

(: TODO: Die erste Grußformel aus dem quoteSalute Korpus holen :)
return (collection($data)//tei:TEI)[3]
```

## Lösungsstrategien

1. Öffnen Sie die Datei `abfrage-challenge-01.xql` mit eXide.
2. Schauen Sie sich eine der Dateien im quoteSalute-Korpus an. Der Pfad ist in der `$data`-Variable hinterlegt. Öffnen Sie mit eXide eine Datei aus diesem Pfad. Schauen Sie sich die XML-Struktur an.
3. Identifizieren Sie den Namen des XML-Elements, welches eine Grußformel samt seiner Metadaten umschließt.
4. Passen Sie das `return`-Statement in der XQuery-Datei in eXide an.