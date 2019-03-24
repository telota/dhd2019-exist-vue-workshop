# Challenge 2: Lösung

Hier ist unsere Musterlösung zur [Challenge 2: Neue Grußformel zum Start](08_Challenge_2_-_Neue_Grußformel_zum_Start.md).

**Zugehörige Beispieldatei**: `09_Challenge_2_Solution.html`

Bei jedem Neuladen der Seite wird eine neue Grußformel geholt.

## JavaScript

* Für jede Variable im `data`-Objekt wurde der Prozess des Überschreibens der Werte analog wiederholt.

```js
created() {
  this.$http.get('https://correspsearch.net/quotesalute/abfrage.xql').then(response => {
    this.quote = response.data.quote;
    this.edition = response.data.edition;
    this.title = response.data.title;
    this.url = response.data.url;
    this.license = response.data.license
  });
}
```