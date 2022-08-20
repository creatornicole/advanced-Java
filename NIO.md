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

## Zusammenfassung

- NIO = New Input Output
- ist Erweiterung IOKonzepte in Java
- Compiler schließt Ressource automatisch
- ermöglicht u.a. Datei schnell und einfach zu kopieren, zu verschieben, Änderungen am Dateisystem zu erkennen, Verzeichnisse rekursiv zu durchlaufen und Rechte abzufragen
- stellt Klassen unter java.nio.file bereit, bspw.
  - Path -> repräsentiert Pfad bzw. Datei in System
  - Files -> stellt Routineoperationen wie kopieren und löschen zur Verfügung
