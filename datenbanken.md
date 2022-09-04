# Datenbanken

...über JDBC (Java Database Connectivity) Bibliotheken zur Verfügung gestellt.

- JDBC Bibliotheken sind Reihe von Bibliotheken zur Verbindung mit Datenbanken
- keine universelle Bibliothek für alle Datenbankarten
  - sondern: je Datenbank eine Bibliothek

## JDBC Treiber

...Komponente, die einer Java Anwendung ermöglicht mit einer Datenbank zu interagieren

- JDBC Treibermanager unterliegt Java Anwendung
- Treibermanager unterschiedlich

| Treibermanager                                | Implementation                           |
|-----------------------------------------------|------------------------------------------|
| Native Protokoll Treiber                      | direkte Verbindung zur Datenbank         |
| JDBC Net Treiber                              | DB Middleware <-> Datenbank              |
| JDBC ODBC (Open Database Connectivity) Bridge | ODBC <-> Client Bibliothek <-> Datenbank |
| Native API Treiber                            | Client Bibliothek <-> Datenbank          |

## Java und Datenbanken

1. Verbindungsaufbau zur Datenbank über Verbindungsmechanismus (DB abhängig)
2. SQL-Anweisung senden
3. Anfrageergebnisse verarbeiten
4. Ressourcen wieder freigeben

## places.sqlite

...Datenbank des Browsers mit allen wichtigen Daten des Benutzers.

- wohl wichtigste Datei für forensische Untersuchung des Browsers (für Firefox, Chrome, neuen Edge)

- enthält alle wichtigen Daten eines Benutzers
  - Lesezeichen
  - Chronik (moz_places)
  - Passwörter

- je nach Betriebssystem wird Datei in Unterordner innerhalb Nutzerverzeichnis gespeichert

## Verknüpfung zu Datenbank

1. Einbindung JDBC-Treiber
   - jeweiligen Datenbank-Treiber herunterladen
   - ist Jar-Archiv-Datei
   - in Classpath von Eclipse-Projekt einbinden: Rechtsklick auf Projekt -> _Build path_ -> _Configure Build Path..._ -> Java Build Path -> Librariers -> Classpath -> Add External JARs... ->
   JDBC Treiber Datei in Dateiverzeichnis ausfindig machen und öffnen -> Apply and Close
2. Verbindung zur Datenbank herstellen
   - dafür entsprechenden Treiber über Class-Loader statisch einbinden
   - über Connection-Objekt eigentliche Verbindung einrichten (dafür sqlite-Datei auf Rechner lokalisieren)  


## Auslesen von Informationen aus Datenbank

1. Anfrage an Datenbank senden
   - Statement-Objekt erzeugen
   - Timeout vereinbaren, falls Datenbank nicht reagiert
   - über Methode executeQuery() des Statement-Objektes Anfrage an Datenbank senden
2. Antwort auswerten
   - als Ergebnis der Anfrage erhält man Objekt der Klasse _ResultSet_
   - Objekt auswerten
   - gefundene Datensätze in Textdatei speichern

## Zusammenfassung

- JDBC Bibliotheken zur Verbindung mit verschiedener Datenbanken
- verschiedene Datenbanken benötigen unterschiedliche Bibliothek
- Datenbankenarbeit in Java
  - Verbindungsaufbau über Verbindungsmechanismus
  - Senden SQL-Anweisung
  - Verarbeitung der Anfrageergebnisse
  - Ressourcenfreigabe
