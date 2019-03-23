# VueJS benutzen

In diesem Abschnitt wird kurz beschrieben, was VueJS ist und wie es benutzt werden kann.

**Zugehörige Beispieldatei**: `02_VueJS_benutzen.html`

## Grundlagen

VueJS ist eine JavaScript-Software-Bibliothek, welche sich mit anderen Bibliotheken wie [React](https://reactjs.org/) oder [AngularJS](https://angularjs.org/) vergleichen lässt.

Das grundlegenste Ziel von VueJS ist es, Webseiten reaktiv zu gestalten. Die HTML-Daten werden dabei auf dem Rechner des Nutzers on-the-fly berechnet. Dabei interagieren

* das Datenmodell und
* die VueJS-DOM (VueJS-HTML-Templates)

miteinander. Ändert sich ein Wert im Datenmodell, ändern sich auch alle Anzeigen, wo dieser Wert referenziert ist.

## VueJS im HTML-Dokument

Um VueJS im eigenen JavaScript-Code nutzen zu können, muss es im HTML-Dokument importiert werden. Derzeit ist es gängig JavaScript nicht im `<head>`-Element, sondern am Ende des `<body>`-Tags zu importieren.

Im `body`-Bereich legen wir ein `div`-Element mit der ID `root` an. Dieses soll als Ziel-Element für unsere Vue-Instanz dienen.

```html
<div id="root">
  <!-- Hier kann VueJS zugreifen-->
</div>
```

Wir laden die VueJS-Bibliothek und erstellen eine neue Vue-Instanz. Über den `el`-Parameter teilen wir mit, auf welches Element sich die Vue-Instanz beschränken soll. In diesem Fall das Element mit der ID "root", also `#root`.

```js
const vue = new Vue({
  el: '#root'
});
```

## Code

**Zugehörige Beispieldatei**: `02_VueJS_benutzen.html`

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="css/bootstrap.min.css">
    <title>DHd19: VueJS einbinden</title>
  </head>
  <body>
    <header class="navbar navbar-expand-lg navbar-light bg-light" style="margin-bottom:20px">VueJS einbinden</header>
    <div class="container">
      <div id="root">
        <!-- Hier kann VueJS zugreifen-->
      </div>
    </div>
    <script src="js/vue.js"></script>
    <script>
      const vue = new Vue({
        el: '#root'
      });
    </script>
  </body>
</html>
```