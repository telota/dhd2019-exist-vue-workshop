# Den quoteSalute Korpus abfragen

Die Datenbankabfragen bei quoteSalute werden über die Datei `abfrage.xql` abgewickelt. In diesem Abschnitt wird eine sehr vereinfachte Version dieser Datei erklärt, um die Funktionsweise Schritt für Schritt zu erläutern.

## abfrage.xql - Das quoteSalute-Back-End

1. Öffnen Sie eXide über Ihr eXist-Dashboard. Siehe dazu auch: [Wichtige URLS](01_Erste_Schritte_mit_eXide.md#Wichtige-URLs)
2. Öffnen Sie im [Dateibrowser](01_Erste_Schritte_mit_eXide.md#Aufbau-von-eXide) die Datei `/db/apps/quotesalute/abfrage-tutorial-01.xql`

### Einfache Datenbankabfrage

Der folgende Code-Schnipsel bezieht sich auf die Datei `abfrage-tutorial-01.xql`. Innerhalb von eXist-db wird mit der funktionalen Programmiersprache [XQuery](https://www.w3.org/TR/xquery-31/) gearbeitet. Die dazugehörige Dateiendung ist `.xql`.

Im folgenden Code-Beispiel passiert folgendes:

```xquery
xquery version "3.0";

(: Deklaration von Namensräumen. Wichtig für die Arbeit mit TEI-XML-Daten :)
declare namespace tei="http://www.tei-c.org/ns/1.0";

(: Variable zum Speichern des Daten-Verzeichnispfads :)
let $data := "/db/apps/quotesalute/data"

(: Hole alle TEI-Daten aus dem Korpus :)
return collection($data)//tei:TEI
```

* `(: Kommentar :)` - Angaben die mit `(:` beginnen und `:)` aufhören sind sog. Kommentare. Diese helfen den Code besser zu lesen. Sie haben keinen Einfluss auf den auszuführenden Code.
* Z. 1: Deklaration der XQuery-Version. Dies hilft der eXist-db den Code zu durchleuchten und den möglichen Funktionsumfang des Codes richtig einzuschätzen.
* Z. 3: Es wird der [TEI-Namensraum](https://tei-c.org/release/doc/tei-p5-doc/de/html/ref-namespace.html) deklariert. Namensräume in XML-Daten helfen, den XML-Elementen eine bereits vordefinierte Bedeutung zu verleihen. So wird z.B. mit dem Namensraum-Tag (Element) `<tei:lb/>` sichergestellt, dass es sich um einen Zeilenumbruch (Line Break) handelt, und nicht um eine etwaige Nutzung von `lb` als Gewichtheinheit Pfund.
* Z. 5: Der Pfad zu der Arbeitskollektion von quoteSalute wird in der Variable `$data` hinterlegt.
* Z. 7: Das Ergebnis der gesamten Operation. Hier wird der gesamte quoteSalute-Korpus durchsucht. Dabei sollen alle Elemente aus allen Dateien ausgeliefert werden `//`, die den Tag-Namen `tei:TEI` haben.

### Ergebnisse in eXide

Sie können sich die XML-Ergebnisse direkt in eXide anzeigen lassen.

1. Lesen Sie sich den Code durch
2. Drücken Sie auf den `Eval`-Button in der Toolbar.
3. Es erscheint unter dem Editor-Bereich ein Ergebnisbereich. Dort werden Ihnen die abfragten Daten angezeigt.

Siehe auch [Aufbau von eXide](01_Erste_Schritte_mit_eXide.md#Aufbau-von-eXide).

### Ergebnisse im Browser

Sie können sich die XML-Ergebnisse auch anders über Ihren Browser anzeigen lassen.

1. Öffnen Sie einen neuen Browsertab.
2. Geben Sie folgende URL ein: [http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-01.xql](http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-01.xql).
3. In diesem Fall erhalten Sie noch kein wohlgeformtes XML zurück. Weiter mit Schritt 4.
4. Lassen Sie sich den Seitenquelltext anzeigen um ans rohe XML zu gelangen.
  a. Firefox und Chrome - `Strg + U` oder Rechtsklick -> Seitenquelltext anzeigen.
