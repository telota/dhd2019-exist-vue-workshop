# XML zu JSON

In diesem Abschnitt wird die Erklärung zur Datei `abfrage.xql` erweitert. Es wird gezeigt, wie XML-Daten zu [JSON](https://www.json.org/json-de.html) serialisiert werden können.

## Neuerungen im Code

1. Öffnen Sie die Datei `abfrage-tutorial-03.xql` in eXide.
2. Schauen Sie sich Code und Kommentare an.
3. Führen Sie den Code aus. Lassen Sie sich das Ergebnis in eXide oder im Browser anzeigen. Was hat sich im Vergleich zu `abfrage-tutorial-02.xql` geändert?

## Erläuterungen

Z. 5-8: Wir wollen das XML-Ergebnis am Ende nach JSON serialisieren. Der `output`-Namensraum wird benötigt, um Daten in ein anderes Format zu serialisieren. Mit der Option `exist:serialize` zeigen wir der eXist-db an, dass später im Code eine Datenserialisierung erfolgen soll und die dementsprechenden Funktionen bereitgehalten werden sollen.

```xquery
declare namespace output="http://www.w3.org/2010/xslt-xquery-serialization";

(: Serialisierung nach JSON als Ergebnisziel angeben :)
declare option exist:serialize "media-type=application/json";
```

Z. 10-27: Dies ist eine interne Helferfunktion, welche XML-Daten bereinigt. Dabei wird sämtlicher Textinhalt aus einem Element und seinen Kinderelementen zu einem Text zusammengefügt.

| Vorher   | Nachher   |
|---|---|
| `<div>Das ist <a href="#">das Haus</a> vom Nikolaus.</div>`  | `<div>Das ist das Haus vom Nikolaus.</div>`  |

Schauen wir uns ein Beispielzitat aus dem Korpus an:

```xml
<cit>
    <quote ana="#formal #s-m #r-n" xml:lang="deu">Mit Verehrung Ihr ergebenster
      etc.</quote>
    <bibl>
      <title type="edition">Jean Paul – Sämtliche Briefe digital</title>
      <title type="letter">An Friederike Christiane Elisabeth von Ompteda. Bayreuth, 24. Dezember 1819.</title>
      <ref target="https://jeanpaul-edition.de/brief.html?num=VII_612"/>
    </bibl>
</cit>
```

Z. 46-52: Die Inhalte und Metadaten zur zufällig ausgewählten Grußformel werden in separaten Variablen gespeichert. Dabei werden die Inhalte mit `normalize-space()` und `local:clean-up()` bereinigt, um z.B. Zeilenumbrüche und ggf. doppelt vorkommende Leerstellen zu entfernen. Der Inhalt der Variable `$quote` wird in diesem Fall dann `<quote>Mit Verehrung Ihr ergebenster etc.</quote>` sein. Das gilt analog für die anderen Variablen.

```xquery
let $quote := element quote { normalize-space(string-join(local:clean-up($randomcit/tei:quote))) }
let $edition := element edition { normalize-space($randomcit//tei:title[@type='edition']) }
let $title := element title { normalize-space($randomcit//tei:title[@type='letter']) }
let $language := element language { normalize-space($randomcit//tei:quote/@xml:lang) }
let $url := element url { $randomcit//tei:bibl/tei:ref/@target/data(.) }
let $licence := element licence { $randomcit//tei:licence/@target/data(.) }
```

Z. 54: Wir erstellen ein neues Element `<cit>` mit den bereinigten Inhalten aus den Statements zuvor.

```xquery
let $preparedGreeting := element cit {$quote,$edition,$title,$url,$language,$licence}
```

Der Inhalt von `$preparedGreeting` sollte dann mit dem Beispiel oben wie folgt aussehen:

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

Z. 57-63: Hier werden die JSON-Serialisierungsparameter angegeben. D.h., hier wird bestimmt, wie der JSON-Output am Ende aussehen soll.

```xquery
let $jsonSerializationParams :=
<output:serialization-parameters
        xmlns:output="http://www.w3.org/2010/xslt-xquery-serialization">
    <output:method value="json"/>
    <output:media-type value="application/json"/>
   <output:json-ignore-whitespace-text-nodes value="yes"/>
</output:serialization-parameters>
```

Z. 66-67: Die berenigten XML-Daten in `$preparedGreeting` werden mit den von uns vorgegebenen JSON-Serialisierungsparametern `$jsonSerializationParams` nach JSON umgeformt. 

```xquery
return 
serialize($preparedGreeting, $jsonSerializationParams)
```

Das JSON-Ergebnis sieht wie folgt aus:

```json
{
  "quote":"Mit Achtung der Ihrige",
  "edition":"August Wilhelm Ifflands dramaturgisches und administratives Archiv",
  "title":"Von Johann Gottfried Schadow. Berlin, 12. März 1805. Dienstag",
  "url":"http://iffland.bbaw.de/briefe/detail.xql?id=A0000306",
  "language":"deu",
  "licence":null
}
```

## Code

```xquery
xquery version "3.0";

(: Deklaration von Namensräumen. Wichtig für die Arbeit mit TEI-XML-Daten :)
declare namespace tei="http://www.tei-c.org/ns/1.0";
declare namespace output="http://www.w3.org/2010/xslt-xquery-serialization";

(: Serialisierung nach JSON als Ergebnisziel angeben :)
declare option exist:serialize "media-type=application/json";

(: Helferfunktion um Datenstrukturen zu bereinigen :)
declare function local:clean-up($nodes as node()*) as xs:string* {
    for $node in $nodes
    return
        typeswitch($node)
            case element(tei:lb)|element(tei:abbr)|element(tei:reg)|element(tei:note)
                return
                ()
            case element()
                return
                local:clean-up($node/node())
            case text()
                return
                $node
            default
                return
                local:clean-up($node/node())
    };

(: Variable zum Speichern des Daten-Verzeichnispfads :)
let $data := "/db/apps/quotesalute/data"

let $greetings := collection($data)//tei:cit

(: Wähle eine zufällige Position aus der Ergebnisliste :)
let $random := util:random(count($greetings))

(: Stelle sicher, dass auch wirklich nur ein Ergebnis ausgewählt wurde :)
let $cleanRandom :=
    if ($random >= 1)
    then $random
    else 1

(: Hole die Grußformel an der Stelle :)
let $randomcit := $greetings[position()=$cleanRandom]

(: Erstelle Variablen für die Inhalte und Metdaten zu einer Grußformel :)
let $quote := element quote { normalize-space(string-join(local:clean-up($randomcit/tei:quote))) }
let $edition := element edition { normalize-space($randomcit//tei:title[@type='edition']) }
let $title := element title { normalize-space($randomcit//tei:title[@type='letter']) }
let $language := element language { normalize-space($randomcit//tei:quote/@xml:lang) }
let $url := element url { $randomcit//tei:bibl/tei:ref/@target/data(.) }
let $licence := element licence { $randomcit//tei:licence/@target/data(.) }

let $preparedGreeting := element cit {$quote,$edition,$title,$url,$language,$licence}

(: Bestimmte wie die JSON-Serializierung aussehen soll :)
let $jsonSerializationParams :=
<output:serialization-parameters
        xmlns:output="http://www.w3.org/2010/xslt-xquery-serialization">
    <output:method value="json"/>
    <output:media-type value="application/json"/>
   <output:json-ignore-whitespace-text-nodes value="yes"/>
</output:serialization-parameters>

(: Serialisiere das zufällige XML-cit-Element nach JSON :)
return 
serialize($preparedGreeting, $jsonSerializationParams)

```