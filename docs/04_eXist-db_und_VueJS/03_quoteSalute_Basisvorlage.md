# quoteSalute Basisvorlage

In diesem Abschnitt wird der Grundaufbau der quoteSalute VueJS-App vorgestellt.

**Zugehörige Beispieldatei**: `03_quoteSalute_Basisvorlage.html`

## JavaScript

Im JavaScript-Abschnitt wurde eine neue VueJS-Instanz initialisiert. Diese greift auf den Bereich im HTML-Code mit der ID `#quoteSalute` zu.

```js
<script src="js/vue.js"></script>
<script>
  const vue = new Vue({
    el: '#quoteSalute',
    data: {
      // data noch leer
    }
  });
</script>
```

## HTML

Das Grußformelbeispiel aus dem [vorigen Abschnitt](02_quoteSalute_Datenstruktur.md) wird vorerst hart in den HTML-Code eingetragen. Vergleichen Sie es mit dem XML- und JSON-Code aus dem vorigen Abschnitt.

```html
<div class="card">
  <div class="card-body">
    <h5 class="card-title">Jean Paul – Sämtliche Briefe digital</h5>
    <h6 class="card-subtitle mb-2 text-muted">An Friederike Christiane Elisabeth von Ompteda. Bayreuth, 24. Dezember 1819.</h6>
    <p class="card-text"><em>Mit Verehrung Ihr ergebenster etc.</em></p>
    <a href="https://jeanpaul-edition.de/brief.html?num=VII_612" class="card-link" target="_blank">Zum Originalbrief</a>
  </div>
</div>
```

## Code

**Zugehörige Beispieldatei**: `03_quoteSalute_Basisvorlage.html`

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
              <h5 class="card-title">Jean Paul – Sämtliche Briefe digital</h5>
              <h6 class="card-subtitle mb-2 text-muted">An Friederike Christiane Elisabeth von Ompteda. Bayreuth, 24. Dezember 1819.</h6>
              <p class="card-text"><em>Mit Verehrung Ihr ergebenster etc.</em></p>
              <a href="https://jeanpaul-edition.de/brief.html?num=VII_612" class="card-link" target="_blank">Zum Originalbrief</a>
            </div>
          </div>
        </div>
    </div>
    <script src="js/vue.js"></script>
    <script>
      const vue = new Vue({
        el: '#quoteSalute',
        data: {
          // data noch leer
        }
      });
    </script>
  </body>
</html>

```