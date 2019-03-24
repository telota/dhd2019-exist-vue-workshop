# Aktionen beim Start

In diesem Abschnitt wird vorgestellt, wie bestimmte VueJS-Operationen bereits beim Start der Instanz ausgeführt werden.

**Zugehörige Beispieldatei**: `06_Aktionen_beim_Start.html`

## Eine neue Grußformel

Öffnen Sie die Beispieldatei `06_Aktionen_beim_Start.html`. Warum wird eine neue Grußformel angezeigt?

## created

Neben `data`, `methods` und `computed` gibt es noch weitere Möglichkeiten eine VueJS-Instanz auszugestalten.

Legt man eine `created()` Funktion an, wird der Inhalt dieser Funktion ausgeführt, sobald die VueJS-Instanz vom Browser geladen wurde.

Das untenstehende Beispiel läuft wie folgt ab:

1. Lade das `data`-Element. Der Wert von `quote` ist "Mit Verehrung Ihr ergebenster etc.".
2. Prüfe, ob es eine `created()`-Funktion gibt. Ja, also führe Sie aus.
3. In der `created()`-Funktion wird der Wert von `quote` mit "Eine neue Grußformel".
4. Jetzt ist die VueJS-Instanz bereit zum Rendern.
5. Wie wird die Grußformel lauten, die angezeigt wird?

```js
const vue = new Vue({
  el: '#quoteSalute',
  data: {
    quote: 'Mit Verehrung Ihr ergebenster etc.',
    edition: 'Jean Paul – Sämtliche Briefe digital',
    title: 'An Friederike Christiane Elisabeth von Ompteda. Bayreuth, 24. Dezember 1819.',
    url: 'https://jeanpaul-edition.de/brief.html?num=VII_612',
    language: 'deu',
    license: null
  },
  methods: {
    // ...
  },
  computed: {
    // ...
  },
  created() {
    this.quote = 'Eine neue Grußformel'
  }
});
```