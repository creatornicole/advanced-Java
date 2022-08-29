# Streams

...darunter versteht man Datenströme, über welche der Datenaustausch von Programmen mit Speichermedien, über Netze, zwischen Threads und peripheren Geräten einheitlich abläuft.

## Begriffserklärungen

| Begriff      | Bedeutung                                                                                                   |
|--------------|-------------------------------------------------------------------------------------------------------------|
| Datenstrom   | abstraktes Konstrukt mit Fähigkeit Zeichen auf imaginäres Ausgabegerät zu schreiben und von diesem zu lesen |
| Eingabestrom | Folge von Daten aus Datenquelle in Programm schreiben                                                       |
| Ausgabestrom | Folge von Daten aus Programm in Datensenke lesen                                                            |

## Ein- und Ausgabestrom

- Eingabestrom für schreiben von Daten aus Datenquelle in Programm
  - "Bytes können von mir gelesen werden."
  - hat Lesemethoden
- Ausgabestrom für lesen von Daten aus Programm in Datensenke
  - "Bytes können auf mich geschrieben werden."
  - hat Schreibemethoden

## Verarbeitungsprinzip

- Lesen (Eingabe)\
  _öffne(Strom)_\
  _solange(Daten zu lesen) {_\
    _lies(Daten)_\
    _verarbeite(Daten)_\
  _}_\
  _schließe(Strom)_

- Schreiben (Ausgabe)\
  _öffne(Strom)_\
  _solange(Daten zu schreiben) {_\
    _verarbeite(Daten)_\
    _schreibe(Daten)_\
  _}_\
  _schließe(Strom)_


## java.io hinsichtlich Ein- und Ausgabe

...Paket java.io stellt umfangreiche Bibliothek zur Ein- und Ausgabe dar

### Klassen für verschiedenartige Ströme
  | Klasse       | Nutzen                                 | Standardimplementationen |
  |--------------|----------------------------------------|--------------------------|
  | InputStream  | Eingabestrom für Bytes (= Byte-Stream) |                          |
  | OutputStream | Ausgabestrom für Bytes (= Byte-Stream) |                          |
  | Reader       | Eingabestrom für Zeichen               | BufferedReader           |
  | Writer       | Ausgabestrom für Zeichen               | BufferedWriter           |

- Methoden des InputStream
| Methode            | Erklärung                                                                     |
|--------------------|-------------------------------------------------------------------------------|
| read()             | Liest einen Byte von InputStream                                              |
| read(byte[] array) | Liest Bytes von InputStream und speichert diese in angegebenen Array          |
| available()        | Gibt die Anzahl der Bytes, die im InputStream vorhanden sind, aus             |
| mark()             | Markiert Position in InputStream, bis zu welchen zuletzt Daten gelesen wurden |
| reset()            | Setzt Position auf zuletzt Markierte zurück                                   |
| markSupported()    | Kontrollieren, ob mark() und reset() von InputStream unterstützt werden       |
| skips()            | Überspringt angegebene Anzahl von Bytes des InputStreams                      |
| close()            | Schließt InputStream                                                          |

### Interfaces für bestimmte Funktionalitäten
  | Interface    | Definieren           |
  |--------------|----------------------|
  | DataInput    | Methoden zur Eingabe elementarer Datentypen sowie Zeichenketten |
  | DataOutput   | Methoden zur Ausgabe elementarer Datentypen sowie Zeichenketten |
  | ObjectInput  |                      |
  | ObjectOuput  |                      |
  | Serializable |                      |

### Dienstklassen fpr spezielle Aufgaben
  | Klasse            | Aufgabe                                                                                                                                                                                    |
  |-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
  | File              | ...repräsentieren Java Dateien bzw. Verzeichnisse des Datei-Systems, ermöglichen Zugriff auf wichtigte Dateiattribute/-eigenschaften, dabei kein Bezug zu Dateiinhalt (für Inhalt Streams) |
  | RandomAccessFile  |                                                                                                                                                                                            |   

## Verkettung und Verschachtelung

...sind bei Streams möglich.

| Art             | Definition                                                                                                                                                                    |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Verkettung      | Zusammenfassung von Dateien, Darstellung als einzigen Strom für Aufrufer                                                                                                      |
| Verschachtelung | erlaubt Konstruktion von Filtern, die bei Ein- und Ausgabe bestimmte Zusatzfunktionen übernehmen, bspw.: Puffern von Zeichen, Zählen von Zeilen, Interpretation binärer Daten |

- beide Konzepte mit normalen Sprachmitteln realisiert
  -> können selbst erweitert werden (zum Erstellen eigener Filter zur Analyse des Eingabestroms)

## Byte-Streams

...zum Lesen und Schreiben von Binärdateien.

- für byteorientierte Datenströme (Byte-Streams) sind InputStream und OutputStream abstrakte Superklassen
- abstrakte Superklassen = definieren Eigenschaften und Funktionen zum Erben für andere Klassen
  - bieten Methoden zum Lesen und Schreiben von 8-Bit Werten (Bytes) an
  - aus diesen selbst lassen sich jedoch keine Objekte erzeugen
  - es lassen sich nur Objekte aus bspw. folgenden Beispielkonstruktionen bilden
    - FileInputStream (Daten von Datei lesen)
    - ByteArrayInputStream (zur Eingabe in Programm)
    - FileOutputStream (Daten in andere Datei schreiben)

- Zwei Byte-Streamklassen für Objekt-Serialisierung
  - ObjectInputStream
  - ObjectOuputStream

## Zusammenfassung

- Ein- und Ausgabe ist Datenaustausch
- Datenaustausch erfolgt einheitlich über Datenströme = Streams
- Streams haben Fähigkeit auf imaginäres Ausgabegerät zu schreiben und von diesem zu lesen
- Unterscheidung zweier Ströme
  - Eingabestrom - in Programm schreiben/ Eingabe in Programm
  - Ausgabestrom - aus Programm lesen/ Ausgabe aus Programm
- Verarbeitungsprinzip
  1. Stream öffnen
  2. Solange Daten vorhanden, diese lesen und verarbeiten/ verarbeiten und schreiben
  3. Wenn alle Daten gelesen/geschrieben, Stream wieder schließen
- java.io stellt verschiedene Klassen und Interfaces für Ein- und Ausgabe bereit
  - Klassen für verschiedenartige Ströme: InputStream, OutputStream, Reader, Writer
  - Interfaces für bestimmte Funktionalitäten: DataInput, DataOutput, ObjectInput, ObjectOuput, Serializable
  - Dienstklassen für bestimmte Aufgaben: File, RandomAccessFile
- Streams können verkettet und verschachtelt werden
- InputStream und OutputStream sind _abstrakte Superklassen_ zum Lesen und Schreiben von Binärdateien
