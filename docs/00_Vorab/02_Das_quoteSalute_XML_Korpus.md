# Das *quoteSalute* Korpus

Als „Indikator für die Beziehungen, die der Briefschreiber zu dem -empfänger hat oder zu haben glaubt“ (Ermert 1979: 104) sind und waren Grußformeln wesentliche Elemente der schriftlichen Kommunikation, insbesondere des Briefes. Deshalb bieten die Richtlinien der Text Encoding Initiative (TEI) mit dem Element `<salute>` auch seit langem eine entsprechende Kodierungsmöglichkeit  (TEI-Konsortium 2018). Für *quoteSalute* werden Grußformeln anhand des `<salute>`-Elements aus TEI-XML-kodierten Briefeditionen extrahiert und in die TEI-XML basierte Struktur des *quoteSalute*-Austauschformats konvertiert.

Für jede Breifedition, die in das Korpus integriert werden soll, wird eine XML-Datei angelegt. Diese besteht aus einem `<teiHeader>` mit den Metadaten (zum Beispiel wo die Daten herstammen) und einem `<body>`, der eine Liste aus `<cit>`-Elementen enthält. Jedes `<cit>` enthält dann die Grußformel, sowie Angaben zum ursprünglichen Brief und zur jeweiligen Edition. Eine Tabellen mit detaillierte Informationen über die Struktur der benötigten TEI-XML-Datei, die für eine Einbindung von Grußformeln in *quoteSalute* erforderlich ist, finden Sie in der Dokumentation auf der [Projektwebseite](https://correspsearch.net/quotesalute//index.xql?id=doc&l=de).

Hier ein Beispiel einer Grußformle im Korpus:

    <cit>
            <quote xml:lang="deu" ana="#formal #s-m #r-m">Leb wohl.</quote>
            <bibl>
                <title type="edition">Briefe und Texte aus dem intellektuellen Berlin um 1800</title>
                <title type="letter">Brief von Adelbert von Chamisso an Louis de La Foye (ohne Ort, Ende Oktober 1804)</title>
                <ref
                    target="http://www.berliner-intellektuelle.eu/manuscript?Brief008ChamissoandeLaFoye.xml"
                />
            </bibl>
        </cit>

Anschließenden erfolgt eine manuellen Kuratierung. Die Daten werden von Wiederholungen und unpassenden Inhalten bereinigt und mit weiter semantischer Information angereichert. Letzteres ermöglicht ein späteres Filtern nach:

* Formalität: Informell bzw. freundschaftlich oder formal
* Geschlecht der Korrespondierenden wie es grammatikalisch aus der Quelle hervorgeht: neutral, weiblich oder männlich
* Sprache: bisher sieben verschiedene, darunter Deutsch, Englisch, Italienisch und Latein

Jede Grußformel erhält ein @xml:lang mit der entsprechenden Sprache und ein @ana, welches Informationen über Geschlecht und Grad der Formalität enthält. Das folgende Beispiel zeigt, wie das Tagging zur semantischen Anreicherung der Grußformeln umgesetzt wurde:

    <quote xml:lang="deu" ana="#formal #s-n #r-n">Bis dahin empfiehlt sich Ihrem Wohlwollen hochachtungsvoll</quote>

Die hier getaggte Grußformel ist in deutscher Sprache, von formellem Charakter und impliziert sowohl für Sender und Empfänger kein erkennbares Geschlecht.

Das Korpus von *quoteSalute* umfasst derzeit 981 Grußformeln aus 14 verschiedenen Briefeditionen (Stand März 2019), unter anderem aus den Editionen “Briefe und Texte aus dem intellektuellen Berlin um 1800” (Balliot o.J.), “Digitale Edition der Briefe Erdmuthe Benignas von Reuß-Ebersdorf (1670-1732)” (Prell/Schmidt-Funke 2017) und “DER STURM. Digitale Quellenedition zur Geschichte der internationalen Avantgarde” (Trautmann / Schrade 2018). Alle Editionen haben ihre Daten unter einer freien Lizenzen zur Verfügung gestellt. 

## Literatur

Baillot, Anne (Ed.) (o.J.): Briefe und Texte aus dem intellektuellen Berlin um 1800. Berlin: Humboldt-Universität zu Berlin. www.berliner-intellektuelle.eu/  [letzter Zugriff am 04.10.2018]

Ermert, Karl (1979). Briefsorten. Untersuchungen zu Theorie und Empirie der Textklassifikation. Tübingen: Niemeyer.
Prell, Martin / Schmidt-Funke, Julia (Eds.) (2017): Digitale Edition der Briefe Erdmuthe Benignas von Reuß-Ebersdorf (1670-1732). Jena [Work in Progress]. http://erdmuthe.thulb.uni-jena.de  [letzter Zugriff am 04.10.2018]

TEI Consortium (2018). <salute>. TEI P5: Guidelines for Electronic Text Encoding and Interchange. [Version 3.4.0 23rd July 2018]. http://www.tei-c.org/release/doc/tei-p5-doc/en/html/ref-salute.html [letzter Zugriff am 04.10.2018]

Trautmann, Marjam / Schrade, Torsten (Eds.) (2018): DER STURM. Digitale Quellenedition zur Geschichte der internationalen Avantgarde. Mainz: Akademie der Wissenschaften und der Literatur. https://sturm-edition.de/quellen/briefe.html  [letzter Zugriff am 04.10.2018]


