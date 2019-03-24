# Vue Methods - Funktionen auf Abruf

In diesem Abschnitt wird erklärt, wie man den `methods`-Bereich einer Vue-Instanz benutzt.

**Zugehörige Beispieldatei**: `07_Vue_Methods_-_Funktionen_auf_Abruf.html`

## Methoden nutzen

Im [vergangenen Abschnitt](06_Vue_Models_-_Daten_eingeben.md) wurde gezeigt, wie man das Vue `data` model in HTML-Formularen manipulierbar macht. Dort wurde die Variable "live" beobachtet und aktualisiert.

Hier soll demonstriert werden, die man eine Funktion auf Abruf, z.B. auf einen Button-Klick, einrichtet.

## Ziel

Die Einkaufsliste soll auf einen Button-Klick geleert werden.

## Vorgehen

Wir fügen einen Button im HTML-Code hinzu.

```html
<button class="btn btn-primary">Liste leeren</button>
```

Wir erstellen den `methods`-Bereich in unserer VueJS-Instanz und fügen eine neue Funktion `emptyList()` hinzu.

Wird die Funktion `emptyList()` ausgeführt, wird die Einkaufslistenvariable `shoppingList` geleert, indem die Einträge durch eine leere Liste ersetzt werden.

Innerhalb der Vue-Instanz bezieht sich `this` auf sämtliche Vue-internen Informationen, wie `data`, `methods` und `computed` Properties [(siehe hier)](10_Computed_Properties_-_Immer_auf_dem_aktuellsten_Stand.md)

```js
const vue = new Vue({
  el: '#root',
  data: {
    name: 'Alexander von Humboldt',
    shoppingList: [
      'Bananen',
      'Brot',
      'Schokolade'
    ]
  },
  methods: {
    emptyList() {
      this.shoppingList = [];
    }
  }
});
```

Nun fügen wir zum neuen Button einen Event-Listener hinzu. Mit der Attribut-Direktive `v-on:click` können wir eine Methode angeben.

```html
<button class="btn btn-primary" v-on:click="emptyList">Liste leeren</button>
```

Diese Direktive kann auch verkürzt werden zu `@click`.

```html
<button class="btn btn-primary" @click="emptyList">Liste leeren</button>
```

## Aufgabe

1. Öffnen Sie die Datei `07_Vue_Methods_-_Funktionen_auf_Abruf.html`.
2. Klicken Sie auf den "Liste Leeren"-Button.
3. Wird die Liste bei Ihnen gelöscht?

## Code

**Zugehörige Beispieldatei**: `07_Vue_Methods_-_Funktionen_auf_Abruf.html`

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
            <button class="btn btn-primary" @click="emptyList">Liste leeren</button>
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
        },
        methods: {
          emptyList() {
            this.shoppingList = [];
          }
        }
      });
    </script>
  </body>
</html>

```