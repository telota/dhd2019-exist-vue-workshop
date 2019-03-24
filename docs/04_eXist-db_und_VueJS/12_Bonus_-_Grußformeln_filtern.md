# Grußformeln filtern

In diesem Abschnitt wird gezeigt, wie Filter auf die Grußformel-Abfrage angewendet werden können.

**Zugehörige Beispieldatei:** `12_Challenge_3_-_Solution.html`.

## Datenmodell erweitern

In diesem Beispiel wird ein Filter zum Auswählen der Sprache der Grußformel eingerichtet.

Zuerst erweitern wir das Datenmodell `data` der VueJS-Instanz mit `filterLanguage`.

```js
const vue = new Vue({
  el: '#quoteSalute',
  data: {
    quote: 'Mit Verehrung Ihr ergebenster etc.',
    edition: 'Jean Paul – Sämtliche Briefe digital',
    title: 'An Friederike Christiane Elisabeth von Ompteda. Bayreuth, 24. Dezember 1819.',
    url: 'https://jeanpaul-edition.de/brief.html?num=VII_612',
    language: 'deu',
    license: null,
    // Siehe hier
    filterLanguage: []
  },
  created() {
    this.$http.get('https://correspsearch.net/quotesalute/abfrage.xql').then(response => {
      this.quote = response.data.quote;
      this.edition = response.data.edition;
      this.title = response.data.title;
      this.url = response.data.url;
      this.license = response.data.license
    });
  }
});
```

## Check-Boxen einrichten

Es werden Check-Box-Inputs eingerichtet, für die Sprachen Deutsch, Englisch und Italienisch. Mit `v-model="filterLanguage"`. Mit dem `value`-Attribut fügen wir einen Wert hinzu.

Wird eine Check-Box angeklickt, wird der dazugehörige Wert in das `filterLanguage`-Array geschrieben.

* Keine Haken: `[]`
* nur Deutsch: `['deu']`
* Deutsch und Englisch: `['deu', 'eng']`
* usw.

```html
<div class="card">
  <div class="card-body">
    <h5 class="card-title">Sprache</h5>
    <div class="row">
      <div class="form-check">
        <input type="checkbox" class="form-check-input" id="languageDeu" value="deu" v-model="filterLanguage">
        <label class="form-check-label" for="sender-female">Deutsch</label>
      </div>
      <div class="form-check">
        <input type="checkbox" class="form-check-input" id="languageEng" value="eng" v-model="filterLanguage">
        <label class="form-check-label" for="sender-male">Englisch</label>
      </div>
      <div class="form-check">
        <input type="checkbox" class="form-check-input" id="languageIta" value="ita" v-model="filterLanguage">
        <label class="form-check-label" for="sender-neutral">Italienisch</label>
      </div>
    </div>
  </div>
</div>
```

## Anfrage anpassen mit computed Parameters

Im [Anfangskapitel zu eXist-db](../02_XML_zu_JSON_in_eXist-db/07_Abfragen_mit_Filtern.md) wurde das Filter-Prinzip von quoteSalute im Back-End bereits erklärt.

Bevor die VueJs-Instanz initialisiert wird, legen wir noch eine Liste mit allen verfügbaren Sprachen an.

```js
const allLanguages = ['deu','eng','spa','fra','ita', 'grc', 'lat'];
```

Das Back-End zerlegt mehrere Angaben zu einer Filterkategorie, indem die Werte durch `X` getrennt sind. Der folgende `computed`-Wert `languageParams` verbindetet alle möglichen Spracheinträge mit einem `X`, wenn kein Sprachfilter gesetzt wurde. Wurde jedoch eine oder mehrere Sprachen ausgewählt, verbindet er nur die ausgewählten.

```js
computed: {
  languageParams() {
    if (this.filterLanguage.length) {
      return this.filterLanguage.join('X')
    }
    return allLanguages.join('X');
  }
}
```

In der `fetchSalute()`-Methode teilen wir `vue-http` mit, dass URL-Parameter übergeben werden sollen. `vue-http` passt die Anzufragende URL dann automatisch an.

* Sind keine Filter gesetzt, wird die dann folgende URL abgefragt: [https://correspsearch.net/quotesalute/abfrage.xql?language=deuXengXspaXfraXitaXgrcXlat](https://correspsearch.net/quotesalute/abfrage.xql?language=deuXengXspaXfraXitaXgrcXlat)
* Ist z.B. nur Deutsch ausgewählt, wird folgende URL abgefragt: [https://correspsearch.net/quotesalute/abfrage.xql?language=deu](https://correspsearch.net/quotesalute/abfrage.xql?language=deu)

```js
methods: {
  fetchSalute() {
    this.$http.get('https://correspsearch.net/quotesalute/abfrage.xql', {
      params: {
        language: this.languageParams
      }
    }).then(response => {
      this.quote = response.data.quote;
      this.edition = response.data.edition;
      this.title = response.data.title;
      this.url = response.data.url;
      this.license = response.data.license
    });
  }
},
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

        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Sprache</h5>
            <div class="row">
              <div class="form-check">
                <input type="checkbox" class="form-check-input" id="languageDeu" value="deu" v-model="filterLanguage">
                <label class="form-check-label" for="sender-female">Deutsch</label>
              </div>
              <div class="form-check">
                <input type="checkbox" class="form-check-input" id="languageEng" value="eng" v-model="filterLanguage">
                <label class="form-check-label" for="sender-male">Englisch</label>
              </div>
              <div class="form-check">
                <input type="checkbox" class="form-check-input" id="languageIta" value="ita" v-model="filterLanguage">
                <label class="form-check-label" for="sender-neutral">Italienisch</label>
              </div>
            </div>
          </div>
        </div>

      </div>
    </div>
    <script src="js/vue.js"></script>
    <script src="js/vue-resource.js"></script>
    <script>
      const allLanguages = ['deu','eng','spa','fra','ita', 'grc', 'lat'];
      const vue = new Vue({
        el: '#quoteSalute',
        data: {
          quote: 'Mit Verehrung Ihr ergebenster etc.',
          edition: 'Jean Paul – Sämtliche Briefe digital',
          title: 'An Friederike Christiane Elisabeth von Ompteda. Bayreuth, 24. Dezember 1819.',
          url: 'https://jeanpaul-edition.de/brief.html?num=VII_612',
          language: 'deu',
          license: null,
          filterLanguage: []
        },
        computed: {
          languageParams() {
            if (this.filterLanguage.length) {
              return this.filterLanguage.join('X')
            }
            return allLanguages.join('X');
          }
        },
        methods: {
          fetchSalute() {
            this.$http.get('https://correspsearch.net/quotesalute/abfrage.xql', {
              params: {
                language: this.languageParams
              }
            }).then(response => {
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