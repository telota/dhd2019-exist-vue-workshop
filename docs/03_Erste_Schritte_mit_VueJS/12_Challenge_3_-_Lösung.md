# Challenge 3: Lösung

Hier ist unsere Musterlösung zur [Challenge 3: Mehr Infos mit Computed Properties](11_Challenge_3_-_Mehr_Infos_mit_Computed_Properties.md).

## JS

Im `computed`-Bereich wurde eine neue Computed Property `numberOfItems` angelegt.

```js
computed: {
  isValidNewItem() {
    if (this.shoppingList.includes(this.newItem) || this.newItem.length === 0) {
      return false;
    }

    return true;
  },
  // TODO - hier neue Computed Property anlegen
  numberOfItems() {
    return this.shoppingList.length;
  }
}
```

## HTML

Die Anzahl der Einkaufslisteneinträge wird hier gezeigt:

```html
Meine Einkaufsliste <span>({{ numberOfItems }}) </span>lautet:
```

Die Zusatzinformation, ob ein neuer Eintrag noch leer oder bereits in der Einkaufsvorhanden ist, wurde folgendermaßen gelöst. Es folgt dem gleichen Schema wie der Button-Deaktivierung aus dem [Abschnitt zu Computed Properties](10_Computed_Properties_-_Immer_auf_dem_aktuellsten_Stand.md).

```html
<div>
    <label>Neuer Wunsch:</label>
    <input type="text" v-model="newItem">
    <button class="btn btn-info" @click="addItem" v-bind:disabled="!isValidNewItem">Hinzufügen</button>
</div>
<!-- TODO - Hier Info anzeigen, wenn die Eingabe nicht gültig ist-->
<div v-if="!isValidNewItem">
    Neuer Eintrag leer oder bereits vorhanden
</div>
```

## Code

**Zugehörige Beispieldatei**: `12_Challenge_3_-_Solution.html`

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
            Meine Einkaufsliste <span>({{ numberOfItems }}) </span>lautet:
            <!-- TODO - Hier die Anzahl der Listeneinträge anzeigen lassen -->
            <ul>
              <li v-for="item in shoppingList">{{ item }}</li>
              
            </ul>
            <button class="btn btn-primary" @click="emptyList">Liste leeren</button>
            <div>
                <label>Neuer Wunsch:</label>
                <input type="text" v-model="newItem">
                <button class="btn btn-info" @click="addItem" v-bind:disabled="!isValidNewItem">Hinzufügen</button>
            </div>
            <!-- TODO - Hier Info anzeigen, wenn die Eingabe nicht gültig ist-->
            <div v-if="!isValidNewItem">
                Neuer Eintrag leer oder bereits vorhanden
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
          newItem: '',
        },
        methods: {
          emptyList() {
            this.shoppingList = [];
          },
          addItem() {
            if (this.newItem.length && !this.shoppingList.includes(this.newItem)) {
              this.shoppingList.push(this.newItem);
              this.newItem = '';
            }
          }
        },
        computed: {
          isValidNewItem() {
            if (this.shoppingList.includes(this.newItem) || this.newItem.length === 0) {
              return false;
            }

            return true;
          },
          // TODO - hier neue Computed Property anlegen
          numberOfItems() {
            return this.shoppingList.length;
          }
        }
      });
    </script>
  </body>
</html>
```