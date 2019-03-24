# Challenge 1: Anzeige mit Bedingungen

## Aufgabe

Versuchen Sie den VueJS-HTML-Code so anzupassen, dass nur Gegenstände von der Einkaufsliste angezeigt werden, wenn sie mit `'B'` beginnen. Wenn der Gegenstand nicht mit `'B'` beginnt, soll der Eintrag mit `Geheim!` ersetzt werden.

**Zugehörige Beispieldatei**: `04_Challenge_1.html`

## Lösungsstrategien

* Mit dem `v-if`-Attribut kann eine Bedingung formuliert werden.
* Eine Alternative kann mit dem `v-else`-Attribut angegeben werden.
* `v-if` kann im selben Element wie `v-for` vorkommen.
* Siehe auch: [Vue: Conditional Rendering](https://vuejs.org/v2/guide/conditional.html) (engl.)

Zum Beispiel:

```html
<!-- angenommen: anzahl = 3 -->
<div>
  Ich möchte {{ anzahl }} 
  <span v-if="anzahl > 1">Bücher</span>
  <span v-else>Buch</span>
  kaufen
</span
```

* Mit der JavaScript-Funktion `startsWith` können Sie überprüfen, ob eine Zeichenkette mit einem bestimmten Buchstaben beginnt. Wenden Sie diese Funktion auf `item` an.

```js
const name = 'Alexander von Humboldt';
name.startsWith('A') // true
```
