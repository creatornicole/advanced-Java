# Sortieren

## Einfache Sortieralgorithmen

- Prinzip: Werden beim Überprüfen eines Arrays Nachbarelemente in falscher Reihenfolge gefunden, so werden sie vertauscht.

| Algorithmus    | Prinzip                                                                                                        | Aufwand              | Verbesserungsmöglichkeiten                                         |
|----------------|----------------------------------------------------------------------------------------------------------------|----------------------|--------------------------------------------------------------------|
| Bubble-Sort    | größte Element in Abschnitt an letzte Position in Abschnitt bringen                                            | O(n^2) = quadratisch | aufhören, wenn in einem Durchlauf keine Elemente getauscht wurden  |
| Selection-Sort | Sortieren durch Auswahl des i.kleinsten Elements für die Position i des Arrays                                 | O(n^2) = quadratisch |                                                                    |
| Insertion-Sort | Sortieren durch Einfügen des nächsten Elements in ein bereits sortiertes Teil-Array an der richtigen Stelle    | O(n^2) = quadratisch |                                                                    |

- Aufwand bei einfachen Sortieralgorithmen immer quadratisch, da im ungünstigsten Fall jedes Element mit jedem anderen verglichen wird.

## Bubble-Sort

...füge größtes Element der noch unsortierten Elemente an letzte Position in Abschnitt ein.

1. Erster Durchlauf: Array komplett durchlaufen, größte Element an letzte Position in Array verschieben
2. Zweiter Durchlauf: Array bis zum vorletzten Platz durchlaufen, davon größte (also in 2. Durchlauf zweitgrößte) Element an letzte Position in durchlaufenen Abschnitt (also in 2. Durchlauf an vorletzte Position) bringen
3. ...
4. (n-1). Durchlauf: Letzten beiden Element vergleichen und ggf. vertauschen

## Selection-Sort

...in jedem Schritt kleinste (größte) der noch ungeordneten Elemente suchen und am rechten Ende der bereits sortierten Elemente einordnen.

- ob größte oder kleinste Element suchen, ist davon abhängig, ob man diese auf- oder absteigend sortieren will
  - aufsteigend: kleinste Element suchen
  - absteigend: größte Element suchen

- [sortierter Bereich][unsortierter Bereich]
  - k erste Position im noch unsortierten Bereich
  - i Position des kleinsten/größten Elements im noch unsortierten Bereich
  - Element an Stelle k mit Element an Stelle i tauschen
- un-/sortierter Bereich ändert sich pro Durchlauf
  - sortierter Bereich wird immer um ein Element größer
  - unsortierter Bereich wird immer um ein Element kleiner

## Insertion-Sort

...nimm beliebiges Element der noch nicht sortierten Daten auf und ordne es an der richtigen Stelle ein.

- auch hier bildet sich sortierter und unsortierter Bereich

## Effiziente Sortieralgorithmen

...funktionieren nach dem "Teile und Herrsche" Prinzip.

- Aufwand im ungünstigsten Fall: O(n * log2n);

## "Teile und Herrsche" Prinzip

...ist ein allgemeines rekursives Lösungsprinzip für "zerlegbare" Probleme.

- falls Problem "elementar" lösbar, bestimme die Lösung
- falls nicht, so zerlege Problem in gleichartige Teilprobleme und löse sie nach dem gleichen Prinzip
- setze aus Lösungen der Teilprobleme die Gesamtlösung zusammen

## "Teile und Herrsche" Prinzip von Sortieraufgaben

- sortieren von einelementigen und leeren Arrays ist trivial
- zerlege größere Arrays in (zwei) kleinere Teilarrays
- diese Teilarrays sortieren
- sortierten Teilarrays in sortierte Array zusammensetzen

## Merge Sort

...Sortieren durch Mischen.

- Idee
  - Darstellung Teilarrays als Abschnitte des Arrays zwischen zwei Indizes _links_ und _rechts_
  - (Teil)Array in zwei (annhähernd) gleiche Teile geteilt, durch Berechnung des Index in der Mitte (= (links + rechts) / 2) (= Partitionieren)
  - Teilarrays sortieren
  - sortierten Teilarrys in Hilfsarray so "mischen", sodass dabei die Sortierung erhalten bleibt (= Mischen)

- Aufwand: O(n * log2n)

- Nachteil: zusätzlicher Speicherplatz von der Größe des Arrays erforderlich

## Quick-Sort

...Zerlegen des Arrays anhand Pivot Element in zwei Teilarrays.

- vom linken Rand aus: _erste_ Element des Arrays, das größer oder gleich dem Pivot-Element ist
- vom rechten Rand aus: _erste_ Element des Arrays, das kleiner oder gleich dem Pivot-Element ist
- beide Elemente vertauschen
- Prozess fortsetzen, bis man sich trifft
- dort, wo man sich trifft, wird Array geteilt
  - Elemente des linken Teilarrays sind kleiner oder gleich der Elemente des rechten Teilarrays
- Sortieren der Teilarrays, wodurch Gesamtarray automatisch sortiert ist

- Wahl Pivot-Element
  - entscheidet über Aufwand
    - entstehen durch Wahl Pivot-Element ungefähr gleich große Teilarrays, so Aufwand siehe Merge-Sort (O(n * log2n))
    - im ungünstigsten Fall (Teilarray enthält nur Pivot-Element), so ist Aufwand O(n^2)
  - oft wird Rand- oder Mittelelement genommen

- Vorteil: sortiert "in situ" (in place), benötigt nur einen zusätzlichen Speicherplatz zum Vertauschen

## Spezielle Sortierverfahren

...beruhen nicht auf dem Vergleichen von Zahlen oder Objekten, sondern auf Verteilen und Wiederaufsammeln.

- für Werte aus Bereich der ganzen Zahlen: Count Sort
- für Zeichenfolgen fester Länge: Radix-Sort

## Count Sort

...ist ein spezielles Sortierverfahren, welches Werte aus Bereichen der ganzen Zahlen, durch Zählen des Vorkommens sortiert.

- in Hilfsarray zählt man, wie oft jede Zahl in dem zu sortierenden Array vorkommt
- entsprechend wie oft man Zahl gezählt hat, schreibt man diese zurück
- verlangt einmaliges, lineares Durchlaufen durch Array
  - erfordert so viele Schritte, wie Array-Elemente vorhanden sind

- Größe Hilfsarray ergibt sich aus Maximum der sortierenden Werte

- Aufwand: linearer Aufwand O(n)

## Radix-Sort

...ist ein spezielles Sortierverfahren, welches Zeichenfolgen fester Länge durch das Verteilen auf Fächer sortiert.

- jedes mögliche Zeichen erhält eigenes Fach
- für jede Stelle findet Verteilungslauf und anschließender Sammellauf statt
  - für "niedrigste" Stelle zuerst, für "höchste" Stelle zuletzt
  - Verteilungslauf -> für Stelle i wird die Zeichenfolge auf das Fach für das Zeichen an dieser Stelle verteilt
  - Sammellauf -> Zeichenfolgen werden aus den Fächern unter Beibehaltung ihrer relativen Reihenfolge entnommen


## Zusammenfassung

- Einfache Sortieralgorithmen
  - Prinzip: Werden beim Überprüfen eines Arrays Nachbarelemente in falscher Reihenfolge gefunden, so werden sie vertauscht
  - Aufwand: O(n^2)
  - Bubble-Sort -> größte Element in Abschnitt an letzte Position in Abschnitt bringen
  - Selection-Sort -> Sortieren durch Auswahl des i.kleinsten Elements für die Position i des Arrays
  - Insertion-Sort -> Sortieren durch Einfügen des nächsten Elements in ein bereits sortiertes Teilarray an der richtigen Stelle
- Effiziente Sortieralgorithmen
  - Prinzip: "Teile und Herrsche"
  - Aufwand: O(n * log2n)
  - Merge Sort -> Sortieren durch Mischen
  - Quick-Sort -> sortieren, indem man zu allererst Array anhand eines Pivot-Elements in zwei Teilarrays zerlegt
- Spezielle Sortierverfahren
  - Count-Sort -> sortiert Werte durch Zählen des Vorkommens , Aufwand: O(n)
  - Radix-Sort -> sortiert Zeichenfolgen fester Länge durch Verteilen auf Fächer
