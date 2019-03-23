# Challenge 2: Lösung

Hier ist unsere Musterlösung zur [Challenge 2](08_Challenge_2_-_Ein_neuer_Filter.md).

## Erläuterung

Analog zu den anderen Filtern wurde der Sprach-Parameter für eine spätere Datenbankabfrage aufbereitet:

```xquery
(: START - Sprachfilter vorbereiten :)
let $language-contains :=
    for $item in tokenize($language, 'X')
        return concat('contains(.//@xml:lang, "', $item, '")')

let $filter-language :=
     if (count($language) >= 1) then
        let $containQuery := string-join($language-contains, ' or ')
        return concat('[', $containQuery, ']')
     else ()
(: ENDE - Sprachfilter vorbereiten :)
```

Anschließend wurde die `$query`-Datenbankabfragevariable erweitert.

```xquery
let $query := ('collection($data)//tei:cit'||$filter-type||$filter-sender||$filter-receiver||$filter-language)
```

Ruft man nun [http://localhost:8080/exist/apps/quotesalute/abfrage-challenge-02-solution.xql?language=eng](http://localhost:8080/exist/apps/quotesalute/abfrage-challenge-02-solution.xql?language=eng) auf, erscheinen nur Grußformeln auf Englisch.