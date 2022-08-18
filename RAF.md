# RAF

...Random Access File ist eine Dienstklasse des java.io Package, welche den wahlfreien Zugriff auf eine Datei zur Ein- und Ausgabe ermöglicht.

- ermöglicht beliebiges Umherspringen in Datei
- Umherspringen mittels Dateizeiger realisiert
- Lesen/Schreiben beginnt an Position des Dateizeigers
- Dateizeiger verschiebt sich um gelesene bzw. geschriebene Bytes dementsprechend

- auch hier Fehlerbehandlung beachten! (typisch bei Dateiarbeit)

## Vorteile des wahlfreien Zugriffs gegenüber dem sequentiellen Zugriff

- Datei muss nicht komplett von vorne beginnend gelesen werden
- sondern Dateizeiger muss lediglich an entsprechende gewünschte Position gesetzt werden

## Modus "r" und "rw"

- Objekte der Klasse können nur dem Lesen oder dem Lesen und Schreiben dienen
  -> abhängig von Modus "r" oder "rw"

- RAF-Objekt mit Modus "r" erzeugen
  ```java
  RandomAccessFile RAFNurLesen = new RandomAccessFile("Dateiname", "r");
  ```
- RAF-Objekt mit Modus "rw" erzeugen
  ```java
  RandomAccessFile RAFLesenSchreiben = new RandomAccessFile("Dateiname", "rw");
  ```

## Dateizeiger

- auch file pointer genannt
- von Typ _long_
- zeigt auf das Byte, bei dem der nächste Dateizugriff beginnt
- nach Öffnen Datei durch Konstruktur ist Wert des Dateizeigers 0
  -> d.h. zeigt auf erste Byte am Dateianfang
- Erhöhung Wert des Dateizeigers je nach Anzahl der gelesenen bzw. geschriebenen Bytes

- Methoden
  | Methode                                         | Erklärung                                     |
  |-------------------------------------------------|-----------------------------------------------|
  | public long getFilePointer() throws IOException | aktuellen Dateizeiger abfragen                |
  | public void seek(long pos) throws IOException   | Dateizeiger an angegebene Position pos setzen |

## Ein- und Ausgabe

- RAF implementiert Interfaces und durch diese definierte Methoden
  - DataInput -> Ausgabe aus Programm (read-Methoden)
  - DataOutput -> Eingabe in Programm (write-Methoden)
- drei weitere elementare Lesemethoden
  - public int read()
  - public int read(byte[] b)
  - public int read(byte[] b, int off, int len)

## Methoden

| Methode                                                  | Erklärung                                                                                                                      |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| public long length() throws IOException                  | aktuelle Dateigröße abfragen                                                                                                   |
| public void setLength(long newLength) throws IOException | aktuelle Dateigröße neu festsetzen                                                                                             |
| public long getFilePointer() throws IOException          | aktuellen Dateizeiger abfragen                                                                                                 |
| public void seek(long pos) throws IOException            | Dateizeiger an angegebene Position pos setzen                                                                                  |
| public void close() throws IOException                   | schließen einer Datei, gleichzeitig schreiben aller zwischengespeicherten Daten und Freigeben der verwendeten Systemressourcen |



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

- RAF = RandomAccessFile
- Dien0stklasse des java.io Package zum wahlfreien Zugriff auf Datei mittels Dateizeiger
- dafür Dateizeiger an entsprechende Position setzen
