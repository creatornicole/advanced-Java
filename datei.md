# Datei

...ist eine Menge von logisch zusammengehörenden  Daten, die auf einem geeigneten Medium permanent gespeichert werden und über einen Bezeichner identifizierbar sind.

- Dateien kann man sich als Arrays auf einem Speichermedium vorstellen
  -> nächste Zugriff auf Datei wird durch Dateizeiger (file pointer) bestimmt
  -> beim Lesen oder Schreiben wird Zeiger um entsprechende Anzahl Bytes versetzt
- viele Dateien durch spezielle Signaturen erkennbar

## Aufbau

| Teil    | Inhalt                                                                                                |
|---------|-------------------------------------------------------------------------------------------------------|
| Header  | spezifische Dateiinformationen, diese Dateiinformationen können sich von Datei zu Datei unterscheiden |
| Content | eigentlicher Inhalt der Datei                                                                         |
| Footer  | schließt Datei meist ab                                                                               |

## Dateiattribute

...sind im Allgemeinen zusätzliche Informationen, die über den eigentlichen Inhalt hinausgehen.

- werden auch als Metadaten bezeichnet
- unter anderem...
  - Name
  - Typ
  - Ortsinformationen
  - Größe
  - Zeitstempel
  - Rechte
  - Eigentümer

## Möglichkeiten um aus Datei zu lesen

- Scanner
  - scannt Text
  - kann elementare Datentypen und Zeichenketten analysieren
  - nutzt dafür reguläre Ausdrücke

## Zusammenfassung

- Datei ist...
  - Menge von logisch zusammengehörenden Daten
  - permanent auf geeigneten Medium gespeichert
  - identifizierbar über Bezeichner
- Zugriff über Dateizeiger (file pointer)
- Datei besteht aus Header, Content und Footer
- Datei hat Dateiattribute
  - auch als Metadaten bezeichnet
  - neben Dateiinhalt zusätzliche Infos wie: Name, Typ, Ortsinformationen, Größe, Zeitstempel, Rechte, Eigentümer
