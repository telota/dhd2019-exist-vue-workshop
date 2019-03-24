# Vue Models - Daten eingeben

In diesem Abschnitt wird gezeigt, wie man HTML-Formulare ans Vue Datenmodell `data` anbindet.

**Zugehörige Beispieldatei**: `06_Vue_Models_-_Daten_eingeben.html`

## Formulare und VueJS

Im Schritt zu [Data und Templates](03_Data_und_Templates.md) wurde gezeigt, wie man Variablen im `data`-Bereich von VueJS einrichtet und diese im HTML-Code nachnutzt.

Nun soll gezeigt werden, wie man Variablen im `data`-Bereich über HTML-Formulare ändern kann.

Nutzereingaben erfolgen in `<input>`-Elementen. Mit dem `v-model`-Attribut können wir eine `data`-Variable Referenzieren.

Dazu legen wir ein neues Formular an und referenzieren die Namensvariable mit dem Attribut `v-model="name"`.

Immer wenn sich der Wert in dem Input ändern, ändert sich der Wert der Variable im `data`-Bereich.

```html
<label>Namen eingeben:</label><input type="text" v-model="name">
<div>Mein Name ist: {{ name }}</div>
```

## Austesten

1. Öffnen Sie die Datei `06_Vue_Models_-_Daten_eingeben.html` mit einem Browser.
2. Geben Sie einen Namen in das Eingabefeld ein.
3. Beobachten Sie den "Hallo..."-Text. Ändert er sich, während Sie etwas eingeben?

## Code

**Zugehörige Beispieldatei**: `06_Vue_Models_-_Daten_eingeben.html`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="css/bootstrap.min.css">
    <title>DHd19: Challenge 1 - Lösung</title>
  </head>
  <body>
    <header class="navbar navbar-expand-lg navbar-light bg-light" style="margin-bottom:20px">Challenge 1: Lösung</header>
    <div class="container">
        <div id="root">
          <label>Namen eingeben:</label><input type="text" v-model="name">
          <div>Mein Name ist: {{ name }}</div>
          <div>
            Meine Einkaufsliste lautet:
            <ul>
              <li 
                v-for="item in shoppingList"
                v-if="item.startsWith('B')">{{ item }}</li>
              <li v-else>Geheim!</li>
            </ul>
          </div>
        </div>
    </div>
    <script src="js/vue.js"></script>
    <script>
      const vue = new Vue({
        el: '#root',
        data: {
          name: 'Alexander von Humboldt',
          shoppingList: [
            'Bananen',
            'Brot',
            'Schokolade'
          ]
        }
      });
    </script>
  </body>
</html>
```