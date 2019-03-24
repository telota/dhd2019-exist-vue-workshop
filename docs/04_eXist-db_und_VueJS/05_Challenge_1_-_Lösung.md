# Challenge 1: Lösung

Hier ist unsere Musterlösung zur [Challenge 1: Datenstruktur und Templates anlegen](04_Challenge_1_-_Datenstruktur_und_Templates_anlegen.md).

## JavaScript

* Die JSON-Grußformel aus dem vorigen Abschnitt wurde in VueJS-Variablen übersetzt. Nun sind diese Variablen nachnutzbar.

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
  }
});
```

## HTML

Die hartgecodeten Zeichenketten wurden durch die entsprechenden Variablen ersetzt. Statt der Grußformel 

> "Mit Verehrung Ihr ergebenster etc."

wird nun auf die entsprechende Variable `{{ quote }}` zurückgegriffen.

Um die `url`-Variable ans `href`-Attribut anzubinden, wurde die `v-bind`-Direktive, bzw. dessen Kurzform genutzt.

```html
<a v-bind:href="url" class="card-link" target="_blank">Zum Originalbrief</a>
```

```html
<div id="quoteSalute">
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ edition }}</h5>
      <h6 class="card-subtitle mb-2 text-muted">{{ title }}</h6>
      <p class="card-text"><em>{{ quote }}</em></p>
      <a :href="url" class="card-link" target="_blank">Zum Originalbrief</a>
    </div>
  </div>
</div>
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
            </div>
          </div>
        </div>
    </div>
    <script src="js/vue.js"></script>
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
        }
      });
    </script>
  </body>
</html>
```