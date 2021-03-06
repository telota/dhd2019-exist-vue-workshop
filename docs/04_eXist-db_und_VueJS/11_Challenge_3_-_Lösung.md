# Challenge 3: Lösung

Hier ist unsere Musterlösung zur [Challenge 3: Neue Grußformel auf Knopfdruck](10_Challenge_3_-_Neue_Grußformel_auf_Knopfdruck.md).

**Zugehörige Beispieldatei:** `11_Challenge_3_Solution.html`.

Bei Druck auf den `Neu`-Button wird eine neue Grußformel geholt.

## JavaScript

* Der Code zum Abrufen einer neuen Grußformel wurde in die Methode `fetchSalute()` umgelagert.
* In der `created()`-Methode wird `fetchSalute()` einfach aufgerufen.

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
    fetchSalute() {
      this.$http.get('https://correspsearch.net/quotesalute/abfrage.xql').then(response => {
        this.quote = response.data.quote;
        this.edition = response.data.edition;
        this.title = response.data.title;
        this.url = response.data.url;
        this.license = response.data.license
      });
    }
  },
  created() {
    this.fetchSalute();
  }
});
```

## HTML

* Es wurde ein neuer Button eingerichtet.
* Die `fetchSalute()`-Methode wird ausgeführt, wenn er geklickt wird (`v-on:click`).

```html
<button class="btn btn-primary" v-on:click="fetchSalute">Neu</button>
```

## Code

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="css/bootstrap.min.css">
    <title>DHd19: quoteSalute</title>
  </head>
  <body>
    <header class="navbar navbar-expand-lg navbar-light bg-light" style="margin-bottom:20px">quoteSalute</header>
    <div class="container">
        <div id="quoteSalute">
          
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">{{ edition }}</h5>
              <h6 class="card-subtitle mb-2 text-muted">{{ title }}</h6>
              <p class="card-text"><em>{{ quote }}</em></p>
              <a :href="url" class="card-link" target="_blank">Zum Originalbrief</a>
              <div>
                <button class="btn btn-primary" v-on:click="fetchSalute">Neu</button>
              </div>
            </div>
          </div>

        </div>
    </div>
    <script src="js/vue.js"></script>
    <script src="js/vue-resource.js"></script>
    <script>
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
          fetchSalute() {
            this.$http.get('https://correspsearch.net/quotesalute/abfrage.xql').then(response => {
              this.quote = response.data.quote;
              this.edition = response.data.edition;
              this.title = response.data.title;
              this.url = response.data.url;
              this.license = response.data.license
            });
          }
        },
        created() {
          this.fetchSalute();
        }
      });
    </script>
  </body>
</html>

```