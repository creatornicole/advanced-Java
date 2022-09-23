# advanced-Java

## Inhalt
1. Ein-/Ausgabe
   <details>
    <summary>Datei</summary>

    - Dateien wie Array auf Speichermedium
    - Zugriff durch Dateizeiger (file pointer), welcher sich um entsprechende Anzahl Bytes beim Lesen/Schreiben versetzt
    - Möglichkeiten Datei auslesen: Scanner Klasse

   </details>

   <details>
    <summary>Streams</summary>

    - Datenströme, über welche Datenaustausch erfolgt (abstrakes Konstrukt mit Fähigkeit Zeichen auf imaginäres Ausgabegerät zu schreiben und von diesem zu lesen)
    - Eingabestrom = InputStream = Reader
    - Ausgabestrom = OutputStream = Writer

    - Klassen für verschiedenartige Ströme
      - InputStream
      - OutputStream
      - Reader
      - Writer
    - Interfaces für bestimmte Funktionalitäten
      - DataInput
      - DataOutput
      - ObjectInput
      - ObjectOutput
      - Serializable
    - Dienstklassen für bestimmte Aufgaben
      - File
      - RandomAccessFile
    - Byte-Streamklassen zur Objektserialisierung
      - ObjectInputStream (Kindklassen: FileInputStream, ByteArrayInputStream)
      - ObjectOutputStream (Kindklassen: FileOutputStream)


   </details>

   <details>
    <summary>Exceptions</summary>

    - verschiedene IOExceptions beachten!
    - zwei Behandlungsmöglichkeiten
      - Abfangen durch try-catch-Anweisung
      - Weiterleiten durch throws-Deklaration

   </details>

   <details>
    <summary>NIO (New Input Output)</summary>

    - = New Input Output = Ersatz/Erweiterung für IO-Konzepte in Java durch Klassen unter java.nio.file
    - FileSystem
    - Path -> **zentrale Klasse**, repräsentiert Pfad/Datei in System, dadurch ganz einfaches kopieren/verschieben von Datei (auch von Webserver)
    - Files -> zur Verfügung stellen von Routineoperationen wie kopieren und löschen

   </details>
   <details>
    <summary>RAF</summary>

    = Random Access File
    - ermöglicht wahlfreien Zugriff auf Datei zur Ein- und Ausgabe
    - dafür Dateizeiger an entsprechende Position setzen
      - Dateizeiger Typ long
      - zeigt auf Byte, bei dem nächste Dateizugriff beginnt
      - Anfänge elementarer Datenelemente berechenbar
      - Anfänge anderer Datenelemente in extra Index-Datei speichern notwendig
      - getFilePointer() -> Abfrage aktuellen Dateizeigers
      - seek(long pos) -> Dateizeiger an angegebene Position setzen
    - implementiert Interfaces
      - DataInput -> read-Methoden
      - DataOutput -> write-Methoden
    - RAF nach Benutzung schließen

   </details>

   <details>
    <summary>URL und URLConnection</summary>

    - URL-Klasse repräsentiert Ressource im World Wide Web
    - URLConnection-Klasse besitzt Methoden, die einen von der Ressource der URL lesen und auf diesen schreiben lassen
    - Daten einer URL lesen
      - URL-Objekt des Webdokuments erstellen
      - Webdokument.openStream() (ist InputStream zum Auslesen)
      - Files.copy(InputStream in, Path target, CopyOptions option) (zum Kopieren aller Bytes eines InputStreams in Datei)

   </details>

   <details>
    <summary>De-/Serialisierung</summary>

    - um Objekte über Laufzeit hinaus verwenden zu können
    - zu serialisierendes Objekt muss Interface Serializable implementieren
    - Serialisierung ermöglicht Objekte zu speichern
    - Deserialisierung ermöglicht zuvor gespeichertes Objekt zu späteren Zeitpunkt wieder zu laden
    - für Serialisierung Verschachtelung von Streams mit Byte-Streamklassen
      - ObjectOutputStream -> Serialisierung
      - ObjectInputStream -> Deserialisierung

   </details>

2. Suchen/Sortieren
    <details>
     <summary>Suchen</summary>

     - beschränkt sich hier auf Zahlen-Arrays
     - zu lösendes Problem: in Zahlen-Array Index der vorgegebenen Zahl bestimmen
     - zwei Möglichkeiten
       - lineares Durchlaufen -> bei unsortierten Arrays -> Sequentielle/ Lineare Suche
       - Intervall-Teilung -> bei sortierten Arrays -> Binäre Suche

    </details>
    <details>
     <summary>Sortieren</summary>

     - Arrays aus einem oder keinem Element trivialerweise sortiert
     - Einfache Sortieralgorithmen
       - Prinzip: Array Nachbarelemente werden überprüft und gegebenenfalls vertauscht
       - Aufwand immer quadratisch (O(n^2))
       - Beispiele: Bubble-Sort, Selection-Sort, Insertion-Sort
     - Effiziente Sortieralgorithmen
       - Prinzip: "Teile und Herrsche"
       - Aufwand im ungünstigsten Fall: O(n*log2n)
       - Beispiele: Merge-Sort, Quick-Sort
     - Spezielle Sortierverfahren: Count-Sort, Radix-Sort

    </details>
    <details>
     <summary>Aufwand</summary>

     - zur Aufwandsbetrachtung wird Computer als "abstrakte Maschine" idealisiert, bei der alle Operationen die gleiche Zeiteinheit und alle elementaren Daten den gleichen Speicherplatz brauchen
     - Betrachtung von T(n) mit n -> unendlich
     - O-Notation soll dem Ziel dienen, eine möglichst einfache Klassifizierung des Aufwandes für unterschiedliche Algorithmen zu finden

    </details>
    <details>
     <summary>Zeichenkettensuche</summary>
    </details>

    <details>
     <summary>Dijkstra-Algorithmus</summary>

     - mit Wegsuche nach Dijkstra garantiert kostengünstigsten Weg in Graphen berechnen
     - Bedingungen:
       - gerichteter Graph
       - gewichteter Graph
       - Kantengewichte des Graphen sind nicht negativ

    </details>

3. Datenstrukturen
    <details>
     <summary>Bibliotheken</summary>
    </details>
    <details>
     <summary>Collection</summary>
    </details>
    <details>
     <summary>Externe Datenstrukturen</summary>
    </details>
    <details>
     <summary>Listen</summary>
    </details>
    <details>
     <summary>Hashing</summary>
    </details>
4. Bäume/Graphen
    <details>
     <summary>Bäume</summary>
    </details>
    <details>
     <summary>Graphen</summary>
    </details>
    <details>
     <summary>Tiefen-/Breitensuche</summary>
    </details>

## Wichtige Klassen zu Themenbereichen

- Scanner
- FileSystem
- Path
- Files
- File
- RandomAccessFile (implementiert DataInput und DataOutput)
- URL
- URLConnection
- InputStream
- OutputStream
- Reader
- Writer
- ObjectInputStream (Bsp.: FileInputStream)
- ObjectOutputStream (Bsp.: FileOutputStream)

## Wichtige Interfaces zu Themenbereichen

- DataInput
- DataOutput
- ObjectInput
- ObjectOutput
- Serializable

## Referenz

Hauptquelle: Modul 21061 Einführung in die Informatik ||: Weiterführende Programmierung gelehrt von Knut Altroggen an der Hochschule Mittweida
Abbildungen: ebd.
