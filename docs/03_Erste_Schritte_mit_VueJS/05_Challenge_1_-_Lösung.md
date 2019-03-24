# Challenge 1: Lösung

Hier ist unsere Musterlösung zur [Challenge 1: Anzeige mit Bedingungen](04_Challenge_1_-_Anzeige_mit_Bedingungen.md).

```html
<div id="root">
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
```

## Erläuterung

1. Mit dem Vue-Attribut `v-if="item.startsWith('B')` wird geprüft, ob der anzuzeigende Gegenstand in der Einkaufsliste mit `'B'` beginnt. Diese Prüfung wird für jeden Eintrag in der Einkaufsliste vorgenommen.
2. Falls die Prüfung fehlschlägt, greift die `v-else`-Direktive.