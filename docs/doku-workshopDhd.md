# Dokumentation zum Workshop 

Um an *quoteSalute* arbeiten zu können, muss zunächst eXist-db und dann die quoteSalute.DB App installiert werden. In diese Anleitung sind alle notwendigen Schritte beschrieben.

## Schritt 1: eXist-db Installation

### System Voraussetzungen

eXist-db läuft mit Java und funktioniert somit auf allen aktuellen Linux, macOS und Windows Betriebsystemen. Folgende Voraussetzungen sind erforderlich:

* mindestens Java 8 (Installations-Anleitungen finden Sie hier: [Java-Downloads für alle Betriebssysteme](https:/www.java.com/de/download/manual.jsp))
* ca. 200Mb Festplattenkapazität
* ca. 512Mb Arbeitsspeicher

Für einige Schritte sind administrative Rechte erforderlich.

Hinweis: Prüfen Sie vorab, ob Java 8 installiert ist und andere/ältere Versionen von eXist-db vollständig deinstalliert sind.

### Installation

1. Gehen Sie auf [http:/exist-db.org/exist/apps/homepage/index.html](http:/exist-db.org/exist/apps/homepage/index.html) und klicken Sie auf "Download eXist-db".
2. Es wird eine .jar-Datei heruntergeladen mit dem Namen "eXist-db-setup-[version].jar" (z.B. "eXist-db-setup-4.4.0.jar").
3. Gehen Sie in den Downloadordner und führen Sie die .jar-Datei aus:
    * bei Windows und Mac doppelt klicken
    * bei Linux rechtsklick und dann auf "mit Java ausführen" klicken
    * oder über die Kommandozeile: 
    ```java -jar eXist-db-setup-[version].jar```
4. Nun öffnet sich ein Installationsassitent. Wir empfehlen die Standardeinstellungen beizubehalten. Klicken Sie auf "Next". ![alt text](images/1.jpg "eXist-db Installer")
5. Sie werden nach folgenden Schritten gefragt:
    1. Installationsordner: wählen Sie einen Pfad und klicken Sie auf "Next". ![alt text](images/2.jpg "eXist-db installation path") 
    2. Datenordner wählen Sie einen Pfad und klicken Sie auf "Next". ![alt text](images/3.jpg "eXist-db data path") 
    3. Admin Passwort und Memory Einstellungen:
        * geben Sie hier ein Passwort Ihrer Wahl ein. Dieses wird später bei bestimmten Aktionen in eXist-db benötigt. 
        * Hinweis: das Freilassen stellt ein Sicherheitsrisiko dar und ist deshalb nicht zu empfehlen.
        ![alt text](imgages/4b.jpg "eXist-db admin pw") 
    4. Package Installation: Klicken Sie "Next"
        ![alt text](images/5.jpg "eXist-db data path") 
    5. Nun erfolgt die package installation. Klicken Sie anschließend auf "Next" ![alt text](images/7.jpg "eXist-db finished") 
    6. Nun erfolgen weitere Installationen. Klicken Sie anschließend auf "Next". ![alt text](images/9.jpg "eXist-db ...") 
    7. Wählen Sie Ihre präferierten Shortcuts und klicken Sie anschließend auf "Next" ![alt text](images/10.jpg "eXist-db data shortcuts") 
    8. Bei erfolgreicher Installation wird dieses Fenster angezeigt: ![alt text](images/11.jpg "eXist-db data success") 

### eXist-db starten

1. Um eXist-db zu starten, führen Sie die exist.jar in ihrem Installationsordner aus.
2. Es öffnet sich nun ein Fenster: ![alt text](images/13.jpg "eXist-db launching")
3. Das eXist-db Icon findet sich nun in Ihrer Symbolleiste.
4. Zum Öffnen des Menüs klicken Sie auf das Icon ![alt text](images/icon.jpg "icon"). 
5. Klicken Sie auf "install as a Service" falls dies nicht bereits erfolgt ist.

## Schritt 2: quoteSalute.DB App installieren
1. Gehen Sie auf die Webseite https://github.com/telota/dhd2019-exist-vue-workshop/workshopDHd/quoteSalute/releases und speichern Sie die Datei quoteSalute.db-〈version〉.xar lokal ab. 
2. Öffnen Sie das eXist-db Menü (klick auf das Icon in der Symbolleiste) und klicken Sie auf "Open Dashboard". Ihr Standardbrowser (vorzugsweise Firefox oder Chrome) sollte sich nun öffnen und das eXist-db Dashboard anzeigen ![alt text](images/15.jpg "eXist-db dashboard").
3. Geben Sie nun Ihre Admin-Nutzerdaten ein: 
    * User: admin
    * Password: [Ihr Passwort, das Sie bei der Installation vergeben haben]
    ![alt text](images/16.jpg "eXist-db dashboard einloggen")
4. Öffnen Sie die Package Manager App. ![alt text](images/17.jpg "eXist-db package manager")
5. Klicken Sie auf den Button add a package, ziehen Sie die gespeicherte Datei quoteSalute.db-〈version〉.xar in das Fenster Upload Packages oder klicken Sie auf Upload und wählen die xar-Datei über Ihr Dateiexplorer aus und schließen Sie das Fenster Package Manager.
6. Im Dashboard sehen Sie nun die quoteSalute.DB App.


## Weitere Informationen 
* [Java-Downloads für alle Betriebssysteme](https:/www.java.com/de/download/manual.jsp)
* [eXist-db Basic Installation](https:/exist-db.org/exist/apps/doc/basic-installation)
* [eXist-db Troubleshooting](https:/exist-db.org/exist/apps/doc/troubleshooting.xml)
