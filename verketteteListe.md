# Verkettete LIsten

- einfach verkettete lineare Listen lassen sich nur sequentiell durchsuchen, deswegen verschiedenartig ausgebaut
  - einfach verkettete Liste mit Referenzen auf erste und letzte Element
  - doppelt verkettete Liste mit erstem und letztem Hilfselement
  - als Ringliste
- verschiedenartiger Aufbau dient immer dem schnelleren Einfügen eines Elements am Ende der Liste

## Einfach verkettete lineare Listen

...ist eine Aneinanderreihung von Listenelementen (Knoten), welche den Dateninhalt und den Verweis auf das jeweilig nächste Listenelement beinhalten.

- Grundbaustein: Listenelement
  - data -> Dateninhalt
  - next -> Verweis auf nächste Listenelement

- Prinzip
  - jedes Listenelement verweist auf jeweils nächste
  - Zugriff über erste Element (nur sequentielle Suche möglich)
  - letztes Element an "leerem Verweis" erkennbar

- Grundlegende Operationen, einige Beispiele
  - Test auf leere Liste
  - Lesen
  - Einfügen
  - Löschen

## Doppelt verkettete Ringliste

...ist eine Aneinanderreihung von Listenelementen (Knoten), wobei jedes Listenelement neben Inhalt und den Verweis auf das nächste Element auch einen Verweis auf das vorhergehende Listenelement beinhaltet.

- LinkedList des Java-Collection-Frameworks ist als doppelt verkettete Ringliste realisiert

- Grundbaustein: Listenelement
  - data -> Dateninhalt
  - next -> Verweis auf nächstes Listenelement
  - prev -> Verweis auf vorhergehende Listenelement

- Vereinbarungen
  - Dateninhalt _null_ unzulässig (außer Eintrittselement, da dieses sowieso nicht der Datenspeicherung dienen soll -> siehe nachfolgende Stichpunkte)
  - Listenlänge als Attribut gespeichert
  - Eintrittselement _entry_ dient nicht zur Datenspeicherung
  - leere Liste wird durch Eintrittselement _entry_ mit Verweisen auf sich selbst dargestellt

| Vorteil                                                                  | Nachteil                                                   |
|--------------------------------------------------------------------------|------------------------------------------------------------|
| Einfügen am Enden viel schneller (kein komplettes Durchlaufen notwendig) | höherer Speicherbedarf (zwei Referenzen pro Listenelement) |
|                                                                          | höherer Aufwand bei Manipulation der Liste                 |

- Hinweis: komplettes Durchlaufen bei einfacher Liste auch nicht notwendig, wenn Referenz auf Ende dabei ist

## Zusammenfassung

- bei verketteten Listen ist Listenelement Grundbaustein
- Einfach verkettete lineare Liste
  - Listenelement beinhaltet: data, next
  - nur sequentiell Durchlaufen möglich
  - dabei Zugriff über erste Element
- Doppelt verkettete Ringliste
