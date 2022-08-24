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

1. Kleinste Element an 1. Position bringen
2. Zweitkleinste Element an 2. Position bringen
3. ...
4. (n-1)-Kleinste bzw. zweitgrößte Element an (n-1). Position bringen
   - bringt gleichzeitig das größte Element an die letzte Position

- Für Ablauf: im i. Schritt Position des kleinsten Array-Elementes von Position i ab bestimmen
  - dann mit Element an Position i zu vertauschen

- in Durchlauf entsteht sortierter- und unsortierter Bereich
  - diese Bereiche ändern sich pro Durchlauf
  - sortierter Bereiche wir immer um ein Element größer
  - unsortierter Bereich wird immer um ein Element kleiner

## Insertion-Sort

...nimm beliebiges Element der noch nicht sortierten Daten auf und ordne es an der richtigen Stelle ein.

- sortieren durch Einfügen des nächsten Elements in bereits sortiertes Teilarray an der richtigen Stelle
- auch hier bildet sich sortierter und unsortierter Bereich

1. Beginn: erstes Element ist erstes Teilarray
   - ist einelementiges Array
   - einelementige Arrays sind immer sortiert
2. Danach: zweites Element mit ersten Element vergleichen
   - ist <, so erstes Element eine Position nach rechts rücken
   - ist >=, so bleiben Elemente an ihren Positionen
3. Analog i. Element einfügen
   - Vergleich mit (i-1). Element beginnen
   - vorhandene Elemente solange um Position nach rechts rücken, bis i. Element (das einzufügende Element) kleiner ist
   - ist einzufügende Element nicht mehr kleiner als vorhandene Elemente, so ist frei gewordenen Platz der richtige

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
   - d.h. haben Teilarrays mehr als ein Element so spalte diese auch wieder in der Mitte auf
   - dies geht solange weiter, bis daraus entstandene Teilarrays aus einem Element bestehen (einelementige Arrays trivialerweise sortiert)
3. Mischen der Teilarrays zu Gesamtarrays
   - beginnt mit einelementigen Teilarrays dessen beiden Elemente sortiert zusammengefügt bzw. "gemischt" Werden
   - geht weiter bis beide Teilarrays entstehen
   - zum letztendlichen Zusammenfügen/"Mischen" der beiden sortierten Teilarrays wird nun zusätzliches Hilfsarray benötigt
   - Elemente werden schrittweise zu Hilfsarray hinzugefügt
   - nächste in Hilfsarray einzuordnende Element ist kleinere der beiden noch nicht einsortierten nächstfolgenden Elemente des Teilarrays
   - sobald Teilarrays leer, so Rest des anderen hinten anfügen
   - Zum Schluss: sortiertes Hilfsarray zu zu sortierendem Array zurückschreiben

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
   - von links: _erste_ Element des Arrays, das größer oder gleich Pivot-Element ist herausfinden
   - von rechts: _erste_ Element des Arrays, das kleiner oder gleich Pivot-Element ist herausfinden
   - diese beiden Elemente vertauschen, da diese jeweils in das andere Teilarray gehören
   - Prozess fortsetzen, bis man sich trifft
   - Stelle an der man aufeinandertrifft = Stelle an der man Array teilt
     - Elemente des linken Teilarrays sind kleiner oder gleich der Elemente des rechten Teilarrays
3. Sortieren der resultierenden beiden Teilarrays (rekursives Verfahren)
   - sortieren Teilarrays hat zur Folge, dass Gesamtarray bei Zusammenfügen automatisch auch sortiert ist

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

...ist ein spezielles Sortierverfahren, welches Werte aus Bereichen der natürlich Zahlen (nichtnegativ, ganz), durch Zählen des Vorkommens sortiert.

- gehört zu sogenannten Verteilungsverfahren
- Array wird genau zweimal durchlaufen
  - erste Mal: Zählen Anzahl der Zahlen
  - zweite Mal: Zurückschreiben Zahlen in zu sortierende Array
  - Aufwand hängt daher linear von der Länge des zu sortierenden Arrays ab
  - erfordert zweimal so viele Schritte, wie Array-Elemente vorhanden sind

1. Anlegen Hilfsarray
2. In Hilfsarray zählen, wie oft Zahl i unter zu sortierenden Zahlen vorkommt
   - Anzahl Zahl i speichert man im Hilfsarray zaehler[i]
3. Von i=0 ausgehend: jeden Index i sooft in zu sortierende Array zurückschreiben, wie es zaehler[i] aussagt

- Größe des Hilfsarray muss zuvor festgelegt werden
  - entweder obere Schranke der zu sortierenden Zahlen festlegen
  - oder vor Sortieren Maximum der zu sortierenden Zahlen ermitteln (erfordert auch nur linearen Aufwand)

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
