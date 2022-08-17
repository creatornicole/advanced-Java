# Exceptions

...oder auch Ausnahmefehler treten bei allen Konstruktoren und den meisten Methoden der Klassen des java.io Paket zur Ein- und Ausgabe von Daten auf.

- bei Ein- und Ausgabe oftmals (eine Form von) IOExceptions

## Fehlerbehandlung

- Abfangen mit try-catch-Anweisung
- Weiterleiten durch throws-Deklaration

## Hierarchie der Exceptions

- Exceptions
  - DataFormatException
  - RuntimeException
  - IOException
    - EOFException
    - FileNotFoundException
    - InterruptedIOException
    - ...
  - ...
## Zusammenfassung

- bei Dateiarbeit (E/A) zwingend Exceptions (vor allem IOExceptions = Input-Output-Exceptions) beachten
- Exceptions erfordern Fehlerbehandlung
- zwei Varianten der Fehlerbehandlung
  - Abfangen mit try-catch
  - Weiterleiten mit throws
- IOException ist Form von Exceptions und unterteilt sich weiter in u.a.
  - EOFException
  - FileNotFoundException
  - InterruptedIOException
- weitere Beispiel-Exceptions, die bei Arbeit mit Dateien auftreten können
  - DataFormatException
  - RuntimeException
