# Challenge 2: Ein neuer Filter

Im [Abschnitt zuvor](07_Abfragen_mit_Filtern.md) wurden Filter zu Höflichkeit, Sender und Empfänger eingerichtet. In dieser Challenge soll ein Sprach-Filter hinzugefügt werden.

## Aufgabe

Erweitern Sie die Datei `abfrage-challenge-02.xql`. Fügen Sie einen Sprach-Filter hinzu. Orientieren Sie sich dabei an die bisherigen Filter.

Überprüfen Sie, ob Ihr Code funktioniert, indem Sie folgende URL im Browser aufrufen: [http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql?language=eng](http://localhost:8080/exist/apps/quotesalute/abfrage-tutorial-04.xql?language=eng).

Wenn Sie nach mehrmaligem Neuladen der Seite nur englische Grußformeln angezeigt bekommen, ist ihr Code-Richtig.

## Lösungsansätze

* In der Variable `$language` wird der Sprachwert gespeichert. Dieser kann leer sein, oder z.B. `deu`, `eng` oder `ita` sein.
* Führen Sie analog zu den bisherigen Filter-Schritten die Variablen `$language-contains` und `$filter-langauge` ein.
* Erweitern Sie die `$query`-Variable
* Ergebnis im Browser überprüfen.
