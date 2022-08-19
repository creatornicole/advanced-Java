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
## Beispiel Schreiben und Lesen mittels RAF

```java
RandomAccessFile raf = null;
try {
    //RAF zum Lesen und Schreiben anlegen
    raf = new RandomAccessFile("C:\\Dateipfad\\testRAF.txt", "rw");
    //Quadratzahlen 0-100 hineinschreiben
    for(int i = 0; i <= 100; i++) {
      raf.writeDouble(Math.pow(i, 2));
    }
    //Dateizeiger an Dateianfang setzen
    raf.seek(0);
    //Geschriebenen Zahlen wieder auslesen und anzeigen lassen
    while(raf.getFilePointer() < raf.length()) {
      System.out.println(raf.readDouble());
    }
} catch (FileNotFoundException e) {
    e.printStackTrace();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if(raf != null) {
      try {
        raf.close(); //Zugriff zu Ressource wieder schließen
      } catch (IOException e) {
        e.printStackTrace();
      }
    }
}
```

## Beispiel speichern unterschiedlich großer Datenelemente in RAF

- Anfänge der Datenelemente wie bei elementaren Datentypen nicht berechenbar
  - deswegen muss man sich die Anfangspositionen der einzelnen Daten innerhalb der Datei merken
- Anfangspositionen der einzelnen Daten innerhalb Datei in Index-Datei speichern
  - Index-Datei speichert Positionen von Datenelementen, enhält also die Dateizeiger der einzelnen Elemente
    - das i.Element der Index-Datei enhält den Dateizeiger auf das i. Datenelement in der Datei der eigentlichen Daten
- Dateizeiger von Typ long
  -> 8 * i ist Position des i. Dateizeigers in der Index-Datei

```java
/** Uebergebenes String-Array in angegebene Datei schreiben
*
* @param dateiname In zu speichernde Datei
* @param strarr Zu speicherndes String-Array mit Zeichenketten
*/
public static void schreibenIn(String dateiname, String[] strarr) {
  RandomAccessFile raf = null; //Zum Speichern der Daten des String-Arrays
  RandomAccessFile index = null; //Zum Speichern der Dateizeiger
  try {
    raf = new RandomAccessFile("Dateipfad" + ".txt", "rw");
    index = new RandomAccessFile("Dateipfad" + ".idx", "rw");
    //String-Array durchlaufen
    for(int i = 0; i < strarr.length; i++) {
      //Dateizeiger auf i. String-Array Element in Index-Datei speichern
      index.writeLong(raf.getFilePointer());
      //i. String-Array Element in RAF schreiben
      raf.writeUTF(strarr[i]);
    }
  } catch (FileNotFoundException e) {
      e.printStackTrace();
  } catch (IOException e) {
      e.printStackTrace();
  } finally {
    try {
        raf.close();
        index.close();
    } catch (IOException e) {
        e.printStackTrace();
    }
  }
}

/**
* n. Zeichenkette aus Datei ausgeben
*
* @param dateiname Datei aus der gelesen werden soll
* @param n Nummer der zu lesenden Zeichenkette in Datei
* @return Zeichenkette an Position n in Datei
*/
public static String liesAus(String dateiname, int n) {
  RandomAccessFile raf = null;
  RandomAccessFile index = null;
  String str = null;
  //Index ab 1 beginnend setzen
  n--;
  try {
    raf = new RandomAccessFile("Dateipfad" + ".txt", "r");
    index = new RandomAccessFile("Dateipfad" + ".idx", "r");
    //Dateizeiger in Index-Datei an richtige Stelle setzen
    index.seek((long) 8 * n);
    //Dateizeiger fuer Datei mit Daten auslesen
    long idx = index.readLong();
    //Dateizeiger in Datei mit Daten an richtige Stelle setzen
    raf.seek(idx);
    //Zeichenkette an gewuenschter Position n auslesen
    str = raf.readUTF();
  } catch (FileNotFoundException e) {
      e.printStackTrace();
  } catch (EOFException e) {
      e.printStackTrace();
  } catch (IOException e) {
      e.printStackTrace();
  } finally {
    try {
        raf.close();
        index.close();
    } catch (IOException e) {
        e.printStackTrace();
    }
  }
  return str;
}

```


## Zusammenfassung

- RAF = RandomAccessFile
- Dien0stklasse des java.io Package zum wahlfreien Zugriff auf Datei mittels Dateizeiger
- dafür Dateizeiger an entsprechende Position setzen
- Speichern von unterschiedlich großen Datenelementen mithilfe von extra Index-Datei, die Dateizeiger auf Daten enthält
