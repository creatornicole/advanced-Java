# Datenbanken

...über JDBC (Java Database Connectivity) Bibliotheken zur Verfügung gestellt.

- JDBC Bibliotheken sind Reihe von Bibliotheken zur Verbindung mit Datenbanken
- keine universelle Bibliothek für alle Datenbankarten
  - sondern: je Datenbank eine Bibliothek

## JDBC Arten

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

...Datenbanken des Browsers.

- places.sqlite für Firefox, Chrome, neuen Edge
- enthält Infos über bspw.: Browserhistorie (moz_places)
