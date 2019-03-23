# Challenge 1: Lösung

Hier ist unsere Musterlösung zur [Challenge 1](03_Challenge_1_-_Eine_Grußformel_abrufen.md).

```xquery
xquery version "3.0";

(: Deklaration von Namensräumen. Wichtig für die Arbeit mit TEI-XML-Daten :)
declare namespace tei="http://www.tei-c.org/ns/1.0";

(: Variable zum Speichern des Daten-Verzeichnispfads :)
let $data := "/db/apps/quotesalute/data"

(: TODO: Das erste Zitat aus dem quoteSalute Korpus holen :)
return (collection($data)//tei:cit)[1]
```

## Erläuterung

* Das Element, welches alle Informationen zu einem Zitat beinhaltet ist `tei:cit`. Hole alle `tei:cit`-Elemente wird zu `//tei:cit`.
* Die eckigen Klammern am Ende deuten an, welche Position in der Ergebnisliste zurückgegeben werden soll.
  * Vorher: `[3]` - 3. Position
  * Nachher: `[1]` - 1. Position
  