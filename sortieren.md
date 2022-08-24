# Sortieren

...Sortiervorgänge für Datenbestände verbrauchen in der praktischen Datenverarbeitung einen bedeutenden Anteil der verfügbaren Rechenkapazität, weswegen vielfältige Sortierverfahren entwickelt wurden.

- Arrays aus einem oder keinem Element sind trivialerweise sortiert

## Einfache Sortieralgorithmen

- Prinzip: Werden beim Überprüfen eines Arrays Nachbarelemente in falscher Reihenfolge gefunden, so werden sie vertauscht.

| Algorithmus    | Prinzip                                                                                                        | Aufwand              | Verbesserungsmöglichkeiten                                         |
|----------------|----------------------------------------------------------------------------------------------------------------|----------------------|--------------------------------------------------------------------|
| Bubble-Sort    | benachbarte Elemente vertauschen, falls sie in falscher Reihenfolge stehen und somit größte Element in Abschnitt an letzte Position in Abschnitt bringen                                            | O(n^2) = quadratisch | aufhören, wenn in einem Durchlauf keine Elemente getauscht wurden  |
| Selection-Sort | Sortieren durch Auswahl des i.kleinsten Elements für die Position i des Arrays                                 | O(n^2) = quadratisch |                                                                    |
| Insertion-Sort | Sortieren durch Einfügen des nächsten Elements in ein bereits sortiertes Teil-Array an der richtigen Stelle    | O(n^2) = quadratisch |                                                                    |

- Aufwand bei einfachen Sortieralgorithmen immer quadratisch, da im ungünstigsten Fall jedes Element mit jedem anderen verglichen wird.

## Bubble-Sort

...benachbarte Elemente vertauschen, falls sie in falscher Reihenfolge stehen.

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

- sortieren durch Einfügen des nächsten Elements in bereits sortiertes Teilarray an der richtigen Stelle
- auch hier bildet sich sortierter und unsortierter Bereich

1. Beginn: erstes Element ist erstes Teilarray
  1. ist einelementiges Array
  2. einelementige Arrays sind immer sortiert
2. Danach: zweites Element mit ersten Element vergleichen
  1. ist <, so erstes Element eine Position nach rechts rücken
  2. ist >=, so bleiben Elemente an ihren Positionen
3. Analog i. Element einfügen
  1. Vergleich mit (i-1). Element beginnen
  2. vorhandene Elemente solange um Position nach rechts rücken, bis i. Element (das einzufügende Element) kleiner ist
  3. ist einzufügende Element nicht mehr kleiner als vorhandene Elemente, so ist frei gewordenen Platz der richtige

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

...beruht auf der Beobachtung, dass es einfach ist, zwei sortierte Listen zu einer sortieren Gesamtliste zu mischen.

- sortieren durch "mischen"
  - teilen Array in zwei Teilarrays
  - Teilarrays separiert voneinander sortieren
  - sortierte Teilarrays zum Schluss zu sortieren Gesamtarray mischen
- rekursives Verfahren (ruft sich sozusagen immer wieder selbst auf)
- Teilarrays werden als Abschnitte des zu sortierenden Arrays zwischen zwei Indizes _links_ und _rechts_ dargestellt
- Mischen der beiden sortierten Teilarrays in zusätzlichen Hilfsarray

1. Wenn Array mehr als ein Element hat, so spalte es in der Mitte auf (mitte = (links + rechts) / 2) (= Partitionieren)
2. Rekursiv so weiter
  1. d.h. haben Teilarrays mehr als ein Element so spalte diese auch wieder in der Mitte auf
  2. dies geht solange weiter, bis daraus entstandene Teilarrays aus einem Element bestehen (einelementige Arrays trivialerweise sortiert)
3. Mischen der Teilarrays zu Gesamtarrays
  1. beginnt mit einelementigen Teilarrays dessen beiden Elemente sortiert zusammengefügt bzw. "gemischt" Werden
  2. geht weiter bis beide Teilarrays entstehen
  3. zum letztendlichen Zusammenfügen/"Mischen" der beiden sortierten Teilarrays wird nun zusätzliches Hilfsarray benötigt
  4. Elemente werden schrittweise zu Hilfsarray hinzugefügt
  5. nächste in Hilfsarray einzuordnende Element ist kleinere der beiden noch nicht einsortierten nächstfolgenden Elemente des Teilarrays
  6. sobald Teilarrays leer, so Rest des anderen hinten anfügen
  7. Zum Schluss: sortiertes Hilfsarray zu zu sortierendem Array zurückschreiben

- Hauptarbeit: Mischen der sortierten Teilarrays

- Aufwand: O(n * log2n)

- Nachteil: zusätzlicher Speicherplatz von der Größe des Arrays erforderlich

## Quick-Sort

...Zerlegen des Arrays anhand Pivot Element in zwei Teilarrays, die einzeln zu sortieren sind.

- Aufteilung Array mit Hilfe von Pivot-Element
  - je nach Wahl des Pivot-Elements entstehen unterschiedliche Abläufe des Verfahrens
  - oft ist mittlere Element das Pivot-Element
- letztendliche Aufteilung so, dass sämtliche Elemente des linken Teilarrays kleiner als Elemente des rechten Teilarrays sind, sodass, sobald die Teilarrays sortiert sind, auch das Gesamtarray sortiert ist


1. Auswählen "Pivot-Element" (Vergleichselement)
2. Anhand des Pivot-Elements Array aufteilen
  1. von links: nächste Element, das größer oder gleich Pivot-Element ist herausfinden
  2. von rechts: nächste Element, das kleiner oder gleich Pivot-Element ist herausfinden
  3. diese beiden Elemente vertauschen, da diese jeweils in das andere Teilarray gehören
  4. solange Suche nach derartigen Paaren von Elementen, bis man irgendwo im Inneren des Arrays trifft
  5. Stelle an der man aufeinandertrifft = Stelle an der man Array teilt
3. Sortieren der resultierenden beiden Teilarrays (WIE LÄUFT SORTIERUNG AB?!)

NOCH MIT EINBAUEN!:
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

- Hauptarbeit: Aufteilung des zu sortierenden Arrays in Große und Kleine

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
  - Bubble-Sort -> benachbarte Elemente vertauschen, falls sie in falscher Reihenfolge stehen, somit größte nach hinten bringen
  - Selection-Sort -> Sortieren durch Auswahl des i.kleinsten Elements für die Position i des Arrays
  - Insertion-Sort -> sortieren durch Einfügen von Elementen an der richtigen Stelle
- Effiziente Sortieralgorithmen
  - Prinzip: "Teile und Herrsche"
  - Aufwand: O(n * log2n)
  - Merge Sort -> Sortieren durch Mischen
  - Quick-Sort -> sortieren, indem man zu allererst Array anhand eines Pivot-Elements in zwei Teilarrays zerlegt
- Spezielle Sortierverfahren
  - Count-Sort -> sortiert Werte durch Zählen des Vorkommens , Aufwand: O(n)
  - Radix-Sort -> sortiert Zeichenfolgen fester Länge durch Verteilen auf Fächer
