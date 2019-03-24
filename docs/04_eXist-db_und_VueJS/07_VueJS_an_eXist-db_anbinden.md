# VueJS an eXist-db anbinden

In diesem Abschnitt wird gezeigt, wie man mit [vue-resource](https://github.com/pagekit/vue-resource) in einer VueJS-Instanz Daten asynchron von einer eXist-db-Instanz abruft und verarbeitet.

**Zugehörige Beispieldatei**: `03_quoteSalute_Basisvorlage.html`

## vue-resource

Die Funktionalität von VueJS wird durch eine Zusatzbibliothek ab diesem Abschnitt erweitert. Nachdem VueJS importiert wird, importieren wir anschließend [vue-resource](https://github.com/pagekit/vue-resource).

```html
<script src="js/vue.js"></script>
<script src="js/vue-resource.js"></script>
```

vue-resource erlaubt es uns, asynchrone Anfragen (sog. AJAX-Requests) an einen Server zu senden. Während Sie also bereits mit dem Browser eine Webseite geöffnet haben, werden im Hintergrund zusätzliche Informationen vom selben oder anderen Servern geladen, um die Webseite mit neuen Informationen zu füttern.

Wir benutzen vue-resource um neue Grußformeln von unserem quoteSalute-Back-End zu holen und in unserer VueJS-Instanz nutzbar zu machen.