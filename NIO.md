# NIO

...New Input Output stellt einen Ersatz bzw. eine Erweiterung für die IOKonzepte in Java dar.

- Zentrale Klassen (unter java.nio.file)
  - FileSystem
  - Path
  - Files

- Unterstützung des try-ressource-Statements = Compiler kümmern sich automatisch um Schließen der Ressource

## Gelöste Probleme

- Datei schnell und einfach kopieren
- Datei verschieben
- Änderungen durch Dateisystem erkennen
- Verzeichnis rekursiv durchlaufen
- Symbolische Verknüpfung anlegen/ verfolgen
- Ansprechen von FTP, Repositories, ...
- Abfragen von Rechten

## Path

...ist zentrale Klasse der NIO und repräsentiert Pfad bzw. Datei in System.

- ermöglicht Zugriff auf u.a.
  - Name
  - Teilpfade
  - Rootverzeichnis

## Files

...stellt Routineoperationen zur Verfügung.

- Routineoperationen sind bspw.
  - kopieren
  - löschen

| Methode                                                                                                                   | Verwendung                                                                  | Hinweise                                   |
|---------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|--------------------------------------------|
| createDirectory(Path dir)                                                                                                 | Neues Verzeichnis erstellen                                                 |                                            |
| createFile(Path path, FileAttribute<>)                                                                                    | Neue, leere Datei erstellen                                                 | failed, wenn diese bereits existiert       |
| createLink(Path link, Path existing)                                                                                      | Erstellt neuen Link zu existierenden Datei                                  |                                            |
| exists(Path p)                                                                                                            | Trifft Aussage darüber, ob Datei/Verzeichnis existiert                      |                                            |
| notExists(Path path, LinkOption)                                                                                          | Trifft Aussage darüber, ob Datei/Verzeichnis nicht existiert                |                                            |
| copy(Path source, Path target, CopyOptions)                                                                               | Kopiert Source in Target                                                    | Path muss bei beiden Dateinamen beinhalten |
| move(Path source, Path target, CopyOptions)                                                                               | Verschiebt Source zu Target                                                 | Path muss bei beiden Dateinamen beinhalten |
| delete(Path path)                                                                                                         | Löscht angegebene Datei                                                     |                                            |
| deleteIfExists(Path path)                                                                                                 | Löscht angegebene Datei falls diese existiert                               |                                            |
| getLastModifiedTime(Path path, LinkOption)                                                                                | Gibt letzte Bearbeitungszeit aus                                            |                                            |
| getOwner(Path path, LinkOption)                                                                                           | Gibt Besitzer der Datei aus                                                 |                                            |
| setLastModifiedTime(Path path, FileTime time)                                                                             | Setzt neue letzte Bearbeitungszeit                                          |                                            |
| setOwner(Path path, UserPrincipal owner)                                                                                  | Setzt neuen Besitzer der Datei                                              |                                            |
| isDirectory(Path path, LinkOption)                                                                                        | Checkt, ob Datei Ordner ist                                                 |                                            |
| isSameFile(Path path, Path path2)                                                                                         | Checkt, ob zwei Pfade die gleiche Datei lokalisieren                        |                                            |
| newInputStream(Path path, OpenOption)                                                                                     | Öffnet Datei, gibt Inputstream zum Lesen aus der Datei zurück               |                                            |
| newOutputStream(Path path, OpenOption)                                                                                    | Öffnet oder erstellt Datei, gibt Outputstream aus, um in Datei zu schreiben |                                            |
| readAllBytes(Path path)                                                                                                   | Liest alles Bytes aus Datei                                                 |                                            |
| readAllLines(Path path, Charset cs)                                                                                       | Liest alle Zeilen aus Datei                                                 |                                            |
| size(Path path)                                                                                                           | Gibt Größe einer Datei aus                                                  | Ausgabe Größe in Bytes, Form long          |
| write(Path path, byte[] bytes, OpenOption)                                                                                | Schreibt Bytes in eine Datei                                                |                                            |
| write(Path path, Iterable<? extends CharSequence> lines, Charset cs, OpenOption) | Schreibt Textzeilen in Datei           |                                                                             |                                            |


- CopyOptions
  - StandardCopyOption.REPLACE_EXISTING -> Ersetzt Datei bzw. Verzeichnis am Zielort

## Beispiel Datei kopieren mit NIO

```java
public class DateiKopieren {
  public static void main(String[] args) throws IOException {
    Path quelle = Paths.get("D:\\test.txt");
    Path ziel = Paths.get("D:\\test2.txt");
    Files.copy(quelle, ziel, StandardCopyOption.REPLACE_EXISTING); //quelle muss bereits existieren
  }
}
```

## Beispiel Datei verschieben mit NIO

```java
public class DateiVerschieben {
  public static main(String[] args) throws IOException {
    Path pSource = Paths.get("Dateiquellpfad.txt"); //Pfad beinhaltet Datei mit Dateinamen
    Path tSource = Paths.get("Dateizielpfad.txt"); //Pfad beinhaltet Datei mit Dateinamen
    Files.move(pSource, tSource, StandardCopyOption.REPLACE_EXISTING);
  }
}
```

## Beispiel Datei von Webserver in Verzeichnis kopieren mit NIO

- dafür URL-Klasse verwenden um URL-Objekt von Webserver-URL erzeugen zu können
- für URL-Objekt InputStream öffnen
- Daten von InputStream in Zielverzeichnis mit copy() von Files kopieren
  -> copy(InputStream, Zielverzeichnis, StandardCopyOption.REPLACE_EXISTING) kopiert alle Bytes des InputStream in angegebener Datei im Zielverzeichnis

```java
public class DateiKopierenWebserver {
  public static main(String[] args) {
    URL url;
    InputStream ips = null;
    try {
        url = new URL("WebserverURL");
        ips = url.openStream();
        Path pTarget = Paths.get("Dateizielpfad.txt");
        Files.copy(ips, pTarget, StandardCopyOption.REPLACE_EXISTING);
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        try {
          ips.close();
        } catch (IOException e) {
          e.printStackTrace();
        }
    }
  }
}
```

## Zusammenfassung

- NIO = New Input Output
- ist Erweiterung IOKonzepte in Java
- Compiler schließt Ressource automatisch
- ermöglicht u.a. Datei schnell und einfach zu kopieren, zu verschieben, Änderungen am Dateisystem zu erkennen, Verzeichnisse rekursiv zu durchlaufen und Rechte abzufragen
- stellt Klassen unter java.nio.file bereit, bspw.
  - Path -> repräsentiert Pfad bzw. Datei in System
  - Files -> stellt Routineoperationen wie kopieren und löschen zur Verfügung
