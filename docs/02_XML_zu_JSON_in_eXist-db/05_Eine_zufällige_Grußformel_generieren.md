# Eine zufällige Grußformel generieren

In diesem Abschnitt wird die Erklärung zur Datei `abfrage.xql` erweitert. Es wird gezeigt, wie ein zufälliges Element aus einer Ergebniskollektion ausgewählt werden kann.

## Neuerungen im Code

1. Öffnen Sie die Datei `abfrage-tutorial-02.xql` in eXide.
2. Schauen Sie sich Code und Kommentare an.
3. Führen Sie den Code aus. Lassen Sie sich das Ergebnis in eXide oder im Browser anzeigen. Was hat sich im Vergleich zu `abfrage-tutorial-01.xql` geändert?

## Erläuterungen

Z. 9: Wir speichern vorerst alle Ergebnisse in eine Variable `$greetings`.

```xquery
let $greetings := collection($data)//tei:cit
```

Z. 12: Wir zählen erst alle Ergebnisse mit `count($greetings)`. Mit `util:random()` wird dann eine zufällige Zahl zwischen 0 und der Anzahl der Ergebnisse ausgewählt.

```xquery
let $random := util:random(count($greetings))
```

Z. 15-18: XQuery kann mit einer "0. Position" nichts anfangen. Dieser Code-Block stellt sicher, dass die Zufallszahl mindestens `1` ist. In anderen Worten: Wenn die Zufallszahl größer oder gleich 1 ist, liefere die Zufallszahl zurück. Falls nicht (also 0 oder kleiner), liefere 1 zurück.

```xquery
let $cleanRandom :=
    if ($random >= 1)
    then $random
    else 1
```

Z. 21: Wähle die Grußformel an der zufällig bestimmten Position aus der Ergebnisliste

```xquery
let $randomcit := $greetings[position()=$cleanRandom]
```

Z. 24: Liefere die zufällige Grußformel als XML zurück.

```xquery
return $randomcit
```

## Code

```xquery
xquery version "3.0";
(: FLOWR for let order where return :)

(: Deklaration von Namensräumen. Wichtig für die Arbeit mit TEI-XML-Daten :)
declare namespace tei="http://www.tei-c.org/ns/1.0";

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

(: Gib die zufällige Grußformel zurück :)
return $randomcit
```