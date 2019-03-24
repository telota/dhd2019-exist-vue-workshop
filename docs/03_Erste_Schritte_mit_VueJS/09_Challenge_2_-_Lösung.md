# Challenge 2: Lösung

Hier ist unsere Musterlösung zur [Challenge 2: Liste erweitern](08_Challenge_2_-_Liste_erweitern.md).

## JS

* Im `data`-Bereich wurde eine neue Variable `newItem` vergeben.
* Im `methods`-Bereich wurde eine neue Funktion `addItem()` angelegt. Diese wird näher erläutert.
  * `if (this.newItem.length)` - Wenn die Zeichenkette vom neuen Eintrag größer als 0 ist.
  * `if (!this.shoppingList.includes(this.newItem))` - Wenn der Eintrag noch nicht in der Einkaufsliste existiert.
  * `this.shoppingList.push(this.newItem)` - Füge den neuen Eintrag der Einkaufsliste hinzu.
  * `this.newItem = ''` - Setze die Eingabe auf einen leeren String zurück.

```js
addItem() {
if (this.newItem.length && !this.shoppingList.includes(this.newItem)) {
  this.shoppingList.push(this.newItem);
  this.newItem = '';
}
```

Insgesamt könnte der JavaScript-Teil Ihrer Vue-Instanz folgendermaßen aussehen.

```js
const vue = new Vue({
  el: '#root',
  data: {
    name: 'Alexander von Humboldt',
    shoppingList: [
      'Bananen',
      'Brot',
      'Schokolade'
    ],
    // TODO - Hier neue Variable anlegen
    newItem: '',
  },
  methods: {
    emptyList() {
      this.shoppingList = [];
    },
    // TODO - Hier neue Funktion anlegen
    addItem() {
      if (this.newItem.length && !this.shoppingList.includes(this.newItem)) {
        this.shoppingList.push(this.newItem);
        this.newItem = '';
      }
    }
  }
});
```

## HTML

Folgende Elemente wurden hinzugefügt:

* `<input type="text" v-model="newItem">` - Neues Text-Formular-Feld, welches via `v-model` an die `newItem`-Variable gebunden wurde.
* `<button class="btn btn-info" @click="addItem">Hinzufügen</button>` - Neuer Button. Wenn er geklickt wird, wird die Funktion `addItem()` ausgeführt (s.o.).

```html
<div>
  <label>Neuer Wunsch:</label>
  <input type="text" v-model="newItem">
  <button class="btn btn-info" @click="addItem">Hinzufügen</button>
</div>
```

## Code

**Zugehörige Beispieldatei**: `09_Challenge_2_-_Solution.html`

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
    <header class="navbar navbar-expand-lg navbar-light bg-light" style="margin-bottom:20px">Challenge 2: Lösung</header>
    <div class="container">
        <div id="root">
          <label>Namen eingeben:</label><input type="text" v-model="name">
          <div>Mein Name ist: {{ name }}</div>
          <div>
            Meine Einkaufsliste lautet:
            <ul>
              <li v-for="item in shoppingList">{{ item }}</li>
            </ul>
            <button class="btn btn-primary" @click="emptyList">Liste leeren</button>

            <!-- TODO: Hier neuen Input und Button anlegen-->
            <div>
                <label>Neuer Wunsch:</label>
                <input type="text" v-model="newItem">
                <button class="btn btn-info" @click="addItem">Hinzufügen</button>
            </div>
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
          ],
          // TODO - Hier neue Variable anlegen
          newItem: '',
        },
        methods: {
          emptyList() {
            this.shoppingList = [];
          },
          // TODO - Hier neue Funktion anlegen
          addItem() {
            if (this.newItem.length && !this.shoppingList.includes(this.newItem)) {
              this.shoppingList.push(this.newItem);
              this.newItem = '';
            }
          }
        }
      });
    </script>
  </body>
</html>
```