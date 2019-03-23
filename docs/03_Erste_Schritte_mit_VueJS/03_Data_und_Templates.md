# Data und Templates

In diesem Abschnitt wird beschrieben, wie man das Datenmodell in einer VueJS-Instanz verwaltet und im HTML-Code nutzbar macht.

## Data

Die Vue-Instanz ähnelt vom Aufbau einem JSON-Objekt. Das `data`-Element verwaltet das interne Datenmodell der Vue-Instanz. Nach dem Key-Value-Prinzip können hier neue Variablen angelegt werden.

Der data-Variable `name` wird der Wert `Alexander von Humboldt` zugeordnet. Der data-Variable `shoppingList` eine Liste mit den Werten `Bananen`, `Brot` und `Schokolade`.

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
  }
});
```

Zwar sind die Variablen nun vorhanden, jedoch noch nicht angezeigt.

## Templates

Auf die Variablen kann im Vue-Bereich des HTML-Codes nun zugegriffen werden. Mit `{{ variable }}` wird der Wert einer Variable ausgegeben.

`{{ name }}` wird also automatisch mit `Alexander von Humboldt` ersetzt.

Man kann auch über Listen iterieren. Für jeden Eintrag `item` in der Einkaufliste `shoppingList` erstelle ein Listenelement `<li>` und trage dort den Wert von `item` ein.

```html
<li v-for="item in shoppingList">{{ item }}</li>
```

Der gesamte Code-Schnipsel sieht also wie folgt aus.

```html
<div id="root">
  <div>Mein Name ist: {{ name }}</div>
  <div>
    Meine Einkaufsliste lautet:
    <ul>
      <li v-for="item in shoppingList">{{ item }}</li>
    </ul>
  </div>
</div>
```

Wenn Sie die Datei mit Ihrem Browser öffnen, sollte folgender Output zu sehen sein.

> Mein Name ist Alexander von Humboldt.
> Meine Einkaufsliste lautet:
>
> * Bananen
> * Brot
> * Schokolade

## Aufgabe

1. Öffnen Sie die Datei `03_Data_und_Templates.html` mit ihrem Browser (rechtsklick -> Öffnen mit...)
2. Öffnen Sie die Datei `03_Data_und_Templates.html` mit einem Text-Editor.
3. Ändern Sie die Werte im `data`-Element in der Vue-Instanz. Fügen Sie weitere Werte zur Einkaufsliste hinzu.
4. Speichern Sie das HTML-Dokument.
5. Laden Sie die Seite in Ihrem Browser neu. Haben sich die Werte geändert?

## Code

**Zugehörige Beispieldatei**: `03_Data_und_Templates.html`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="css/bootstrap.min.css">
    <title>DHd19: Data und Templates</title>
  </head>
  <body>
    <header class="navbar navbar-expand-lg navbar-light bg-light" style="margin-bottom:20px">Data und Templates</header>
    <div class="container">
        <div id="root">
          <div>Mein Name ist: {{ name }}</div>
          <div>
            Meine Einkaufsliste lautet:
            <ul>
              <li v-for="item in shoppingList">{{ item }}</li>
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