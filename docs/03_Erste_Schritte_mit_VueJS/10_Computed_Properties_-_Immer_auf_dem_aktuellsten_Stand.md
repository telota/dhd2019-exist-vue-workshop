# Computed Properties - Immer auf dem aktuellsten Stand

Im [Abschnitt zuvor](07_Vue_Methods_-_Funktionen_auf_Abruf.md) wurde gezeigt, wie Funktionen auf Abruf, z.B. bei einem Button-Klick, aufgerufen werden können.

Es gibt auch **Computed Properties**, also live-berechnete Werteigenschaften. Diese kann man als Variablen verstehen, sich im Template-Bereich wie ein Wert verhalten, im JavaScript-Bereich jedoch wie eine Funktion funktionieren.

**Kernfunktion:** Ändert sich der Wert eines Werts, der in der `computed`-Funktion referenziert ist, wird diese Funktion neu ausgeführt und ein neuer Wert berechnet.

## Eingaben validieren

In der [Challenge 2](08_Challenge_2_-_Liste_erweitern.md) sollten Eingabemöglichkeiten für neue Einkaufslisteneinträge geschaffen werden.

Wenn die Eingabe jedoch noch leer ist, oder der Einkaufswunsch bereits auf der Liste steht, soll man den Button nicht drücken können. Weiterhin sollte angezeigt werden

## computed-Bereich

Wir erweitern unsere VueJS-Instanz um den `computed`-Bereich. Dieser ähnelt im Aufbau dem `methods`-Bereich.

Dabei legen wir eine computed-property-Funktion `isValidNewItem()`, welches überprüfen soll, ob der neuer Eintrag leer oder bereits vorhanden ist.

```js
 const vue = new Vue({
  el: '#root',
  data: {
    // ...
  },
  methods: {
    // ...
  },
  computed: {
    isValidNewItem() {
      if (this.shoppingList.includes(this.newItem) || this.newItem.length === 0) {
        return false;
      }

      return true;
    },
  }
});
```

* Szenario 1:
  * Einkaufsliste: [Brot, Bananen, Schokolade]
  * Neuer Eintrag: (leer)
  * isValidNewItem: `false`
* Szenario 2:
  * Einkaufsliste: [Brot, Bananen, Schokolade]
  * Neuer Eintrag: Brot
  * isValidNewItem: `false`
* Szenario 3:
  * Einkaufsliste: [Brot, Bananen, Schokolade]
  * Neuer Eintrag: Bier
  * isValidNewItem: `true`

Nun kann `isValidNewItem` wie eine `data`-Variable im HTML-Bereich genutzt werden.

## Variablen an Attribute binden

Man kann einen Button deaktivieren, wenn man ihm das `disabled`-Attribut verleiht.

```html
<button disabled>Hinzufügen</button>
```

Das `disabled`-Attribut soll jedoch nur dann aktiviert sein, wenn `isValidNewItem` nicht `true` ist. Mit `!` können `true` und `false` Werte umgekehrt werden, also `!isValidNewItem`.

Mit der `v-bind`-Direktive kann der Status von `isValidNewItem` an das `disabled`-Attribut gebunden werden

```html
<button v-bind:disabled="!isValidNewItem">Hinzufügen</button>
```

Dieser Ausdruck kann auch verkürzt werden:

```html
<button :disabled="!isValidNewItem">Hinzufügen</button>
```

## Code

**Zugehörige Beispieldatei**: `10_Computed_Properties_-_Immer_auf_dem_aktuellsten_Stand.html`


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
                <button class="btn btn-info" @click="addItem" v-bind:disabled="!isValidNewItem">Hinzufügen</button>
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
        },
        computed: {
          isValidNewItem() {
            if (this.shoppingList.includes(this.newItem)) {
              return false;
            }

            if (this.newItem.length) {
              return true;
            }

            return false;
          },
        }
      });
    </script>
  </body>
</html>
```