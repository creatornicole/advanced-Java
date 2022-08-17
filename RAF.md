# RAF

...Random Access File ist eine Dienstklasse des java.io Package, welche den wahlfreien Zugriff auf eine Datei zur Ein- und Ausgabe ermöglicht.

- ermöglicht beliebiges Umherspringen in Datei
- Umherspringen mittels Dateizeiger realisiert
- Lesen/Schreiben beginnt an Position des Dateizeigers

- auch hier Fehlerbehandlung beachten! (typisch bei Dateiarbeit)

## Vorteile des wahlfreien Zugriffs gegenüber dem sequentiellen Zugriff

- Datei muss nicht komplett von vorne beginnend gelesen werden
- sondern Dateizeiger muss lediglich an entsprechende gewünschte Position gesetzt werden

## Beispiel Schreiben mittles RAF

```java
RandomAccessFile raf = null;
try {
  raf = new RandomAccessFile("HalloWelt.txt", "rw");
  raf.writeUTF("Hallo Welt");
} catch (Exception e) {
  e.printStackTrace();
} finally {
  if(raf != null) {
    try {
      raf.close();
    } catch(IOException ex) {
      ex.printStackTrace();
    }
  }
}
```

## Zusammenfassung

- Dienstklasse des java.io Package zum wahlfreien Zugriff auf Datei mittels Dateizeiger
- dafür Dateizeiger an entsprechende Position setzen
