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
    <summary>Dateiarbeit</summary>
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
    <summary>De-/Serialisierung</summary>
   </details>
2. Suchen/Sortieren
    <details>
     <summary>Suchen</summary>
    </details>
    <details>
     <summary>Sortieren</summary>
    </details>
    <details>
     <summary>Aufwand</summary>
    </details>
    <details>
     <summary>Zeichenkettensuche</summary>
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
- RandomAccessFile (implementiert DataInput und DataOutput)

## Wichtige Interfaces zu Themenbereichen

- DataInput
- DataOutput

## Referenz

Hauptquelle: Modul 21061 Einführung in die Informatik ||: Weiterführende Programmierung gelehrt von Knut Altroggen an der Hochschule Mittweida
Abbildungen: ebd.
