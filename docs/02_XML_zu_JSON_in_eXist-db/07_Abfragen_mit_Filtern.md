# Abfragen mit Filtern

In diesem Abschnitt wird die Erklärung zur Datei `abfrage.xql` erweitert. Es wird gezeigt, wie Daten aus dem quoteSalute nach bestimmten Eigenschaften gefiltert werden können, sodass z.B. nur Grußformeln von Frauen als Absender ausgewählt werden.

## Neuerungen im Code

1. Öffnen Sie die Datei `abfrage-tutorial-04.xql` in eXide.
2. Schauen Sie sich Code und Kommentare an.
3. Führen Sie den Code aus. Lassen Sie sich das Ergebnis in eXide oder im Browser anzeigen. Was hat sich im Vergleich zu `abfrage-tutorial-03.xql` geändert?

Wenn Sie den Code mit eXide ausführen, sollte sich im Ergebnis nichts sichtbares geändert haben. Sie können jedoch URL-Parameter angeben, um Daten zu filtern.

## URL-Parameter

Überfliegen Sie kurz die [Dokumentation von quoteSalute](https://correspsearch.net/quotesalute//index.xql?id=doc&l=de).

### Einzelner Filter - Briefe von Frauen

Sie können über die Browser-URL Parameter (nutzerspezifizierte Werte) an das quoteSalute-Back-End übergeben.

Das grundlegende Prinzip ist folgendermaßen: `[URL]?parameter=wert`. Mit dem `?` wird angezeigt, dass Parameter übergeben werden sollen.

1. Öffnen Sie folgende URL in einem neuen Browser-Tab: [http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql](http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql)
2. Sie sollten eine Grußformel als JSON erhalten.
3. Erweitern Sie die URL mit `?sender=s-f`. (`s` für "sender" und `f` für "female")
4. Ihre URL sollte jetzt [http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql?sender=s-f](http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql?sender=s-f) lauten.
5. Im `title`-Feld sollten Sie nachvollziehen können, dass nur noch Grußformeln von Briefen angezeigt werden, deren Verfasser Frauen waren.
6. Laden Sie den Tab mit `F5` neu, um sich eine andere zufällige Grußformel anzeigen zu lassen.

### Mehrere Filter - Briefe von Frauen an Frauen (oder neutral)

Sie können auch mehrere Parameter über die Browser-URL übergeben.

Das grundlegende Prinzip ist folgendermaßen `[URL]?parameter1=wert1&parameter2=wert2`. Mit dem `&` werden Parameterpaare getrennt.

1. Öffnen Sie folgende URL in einem neuen Browser-Tab: [http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql?sender=s-f](http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql?sender=s-f)
2. Sie sollten eine Grußformel als JSON erhalten.
3. Erweitern Sie die URL mit `&receiver=r-fXr-n`.
4. Ihre URL sollte jetzt [http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql?sender=s-f&receiver=r-fXr-n](http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql?sender=s-f&receiver=r-fXr-n)
5. Anhand der Daten sollten Sie nachvollziehen können, dass nur noch Grußformeln von Briefen angezeigt werden, deren Verfasser Frauen waren und deren Empfänger entweder auch Frauen waren bzw. so formuliert sind, dass sich das Geschlecht des Empfängers nicht bestimmen lässt.
6. Laden Sie den Tab mit `F5` neu, um sich eine andere zufällige Grußformel anzeigen zu lassen.

## Erläuterungen

Z. 12-15: Wir teilen der eXist-db mit, dass die Werte von URL-Parametern in Variablen gespeichert werden sollen, falls diese vorkommen. Zum Beispiel wird in `$sender` der Wert `s-f` gespeichert, wenn die Anfrage von der URL `http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql?sender=s-f` kommt.

Folgende URL-Parameter werden akzeptiert:

* `type` - Höflichkeitsstufe
* `sender` - Geschlecht der absendenden Person
* `receiver` - Geschlecht der empfangenden Person
* `language` - Sprache, in welcher die Grußformel verfasst wurde

```xquery
declare variable $type := request:get-parameter('type', ());
declare variable $sender := request:get-parameter('sender', ());
declare variable $receiver := request:get-parameter('receiver', ());
declare variable $language := request:get-parameter('language', ());
```

Z. 39-76: Hier werden die URL-Parameterwerte für eine Datenbankabfrage aufbereitet, sodass der quoteSalute-Korpus entsprechend gefiltert werden kann.

In dem Code-Schnipsel werden nur `type`, `sender` und `receiver` aufbereitet. Der `langauge`-Filter ist die [nächste Challenge](08_Challenge_2_-_Ein_neuer_Filter.md).

In Code-Blöcken zu `$type-contains`, `$sender-contains` und `$receiver-contains` werden Mehrfachnennungen der URL-Parameter aufbereitet. Z.B. wird aus dem URL-Parameter `?receiver=r-fXr-n` die XQuery-Schnipsel `contains(.//@ana, "#r-f")` und `contains(.//@ana, "#r-n")`.

In den Code-Blöcken zu `$filter-type`, `$filter-sender` und `$filter-receiver` werden diese XQuery-Schnipsel dann zu einer Filter-Datenbankanfrage zusammengefügt. Z.B. entsteht dann folgender Wertschnipsel: `contains(.//@ana, "#r-f") or contains(.//@ana, "#r-n")`. Also liefere nur Grußformeln zurück, welche im `@ana`-Attribut die Werte `#r-f` oder `#r-n` enthalten.

```xquery
(: START - Höflichkeitsfilter vorbereiten :)
let $type-contains :=
    for $item in tokenize($type, 'X')
        let $contain := concat("#", $item)
        return concat('contains(.//@ana, "', $contain, '")')

let $filter-type :=
     if (count($type) >= 1) then
        let $containQuery := string-join($type-contains, ' or ')
        return concat('[', $containQuery, ']')
     else ()
(: ENDE - Höflichkeitsfilter vorbereiten :)

(: START - Absenderfilter vorbereiten :)
let $sender-contains :=
    for $item in tokenize($sender, 'X')
        let $contain := concat("#", $item)
        return concat('contains(.//@ana, "', $contain, '")')

let $filter-sender :=
     if (count($sender) >= 1) then
        let $containQuery := string-join($sender-contains, ' or ')
        return concat('[', $containQuery, ']')
     else ()
(: ENDE - Absenderfilder vorbereiten :)

(: START - Empfängerfilter vorbereiten :)
let $receiver-contains :=
    for $item in tokenize($receiver, 'X')
        let $contain := concat("#", $item)
        return concat('contains(.//@ana, "', $contain, '")')

let $filter-receiver :=
     if (count($receiver) >= 1) then
        let $containQuery := string-join($receiver-contains, ' or ')
        return concat('[', $containQuery, ']')
     else () 
(: ENDE - Empfängerfilter vorberiten :)
```

Z. 78: Bereite eine Abfrage (engl. query) vor, indem die bisher bekannte Anfrage `collection($data)//tei:cit` mit den Filtern erweitert wird. Die `||`-Zeichen bedeuten, dass die Werte der dahinterliegenden Variablen und Ausdrücke an die Abfrage rangefügt werden sollen.

```xquery
let $query := ('collection($data)//tei:cit'||$filter-type||$filter-sender||$filter-receiver)
```

Z. 79: Nun holen wir eine Kollektion an Grußformeln, auf die die Filter passen.

```xquery
let $greetings := util:eval($query)
```

Der Rest der Datei ist wie bisher und folgt derselben Logik.

## Code

```xquery
xquery version "3.0";

(: Deklaration von Namensräumen. Wichtig für die Arbeit mit TEI-XML-Daten :)
declare namespace tei="http://www.tei-c.org/ns/1.0";
declare namespace output="http://www.w3.org/2010/xslt-xquery-serialization";

(: Serialisierung nach JSON als Ergebnisziel angeben :)
declare option exist:serialize "media-type=application/json";

(: Request-Parameter entgegenennehmen. Wenn von einer Webseite eine Anfrage kommt,
 : können nutzerdefinierte Angaben mit überreicht werden. :)
declare variable $type := request:get-parameter('type', ());
declare variable $sender := request:get-parameter('sender', ());
declare variable $receiver := request:get-parameter('receiver', ());
declare variable $language := request:get-parameter('language', ());

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

(: START - Höflichkeitsfilter vorbereiten :)
let $type-contains :=
    for $item in tokenize($type, 'X')
        let $contain := concat("#", $item)
        return concat('contains(.//@ana, "', $contain, '")')

let $filter-type :=
     if (count($type) >= 1) then
        let $containQuery := string-join($type-contains, ' or ')
        return concat('[', $containQuery, ']')
     else () 
(: ENDE - Höflichkeitsfilter vorbereiten :)

(: START - Absenderfilter vorbereiten :)
let $sender-contains :=
    for $item in tokenize($sender, 'X')
        let $contain := concat("#", $item)
        return concat('contains(.//@ana, "', $contain, '")')

let $filter-sender :=
     if (count($sender) >= 1) then
        let $containQuery := string-join($sender-contains, ' or ')
        return concat('[', $containQuery, ']')
     else ()
(: ENDE - Absenderfilder vorbereiten :)

(: START - Empfängerfilter vorbereiten :)
let $receiver-contains :=
    for $item in tokenize($receiver, 'X')
        let $contain := concat("#", $item)
        return concat('contains(.//@ana, "', $contain, '")')

let $filter-receiver :=
     if (count($receiver) >= 1) then
        let $containQuery := string-join($receiver-contains, ' or ')
        return concat('[', $containQuery, ']')
     else ()
(: ENDE - Empfängerfilter vorberiten :)

let $query := ('collection($data)//tei:cit'||$filter-type||$filter-sender||$filter-receiver)
let $greetings := util:eval($query)

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