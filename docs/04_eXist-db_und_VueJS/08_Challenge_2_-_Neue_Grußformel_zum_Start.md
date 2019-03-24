# Challenge 2: Neue Grußformel zum Start

**Zugehörige Beispieldatei**: `08_Challenge_2.html`

Im [vorherigen Abschnitt](07_VueJS_an_eXist-db_anbinden.md) wurde die VueJS-Instanz um `vue-resource` erweitert, sodass man innerhalb einer VueJS-Instanz sog. AJAX-Requests ausführen kann. In der `created()`-Methode wurde bereits ein Skelett angelegt, um von der quoteSalute-API eine neue Grußformel abzurufen.

## Aufgabe

Erweitern Sie die `created()`-Funktion bzw. den AJAX-Request mit `vue-resource` so, dass sämtliche Informationen zu einer Grußformel in den `data`-Variablen gespeichert werden.

## Lösungsansätze

* Öffnen Sie die Datei `08_Challenge_8.html` sowohl mit einem Editor und Browser.
* Wenn das Ergebnis bei jedem Neuladen des Browsertabs anders aussieht, scheint Ihr Ergebnis richtig zu sein.
* Die zu bearbeitenden Stellen im Code sind mit `// TODO` markiert.
* Orientieren Sie sich an der JSON-Datenstruktur.
* Tipp: Nutzen Sie die Entwicklerwerkzeuge Ihres Browsers.
  * Drücken Sie `F12`.
  * Gehen Sie auf den Tab `Netzwerkanalyse`.
  * Klicken Sie auf `XHR`.
  * Laden Sie die Seite neu.
  * Es sollte ein Eintrag erscheinen. Klicken Sie auf diesen.
  * Klicken Sie auf Antwort.
  * Das Ergebnis des asynchronen Requests wird Ihnen dort angezeigt.