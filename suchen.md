# Suchen von Daten

..also das Wiederbeschaffen bestimmter Informationen aus Informationsmengen ist eine zentrale Aufgabe der Datenverarbeitung.

## Suchen in Feldern

...ist stark vereinfachtes Problem der Datensuche.

- Charakteristische: Datenstrukturen sind Zahlen in Array, in Schlüsselwerten identisch

- Problem: in Zahlen-Array Index der vorgegebenen Zahl bestimmen
  - zwei Möglichkeiten, Index der vorgegebenen Zahl zu bestimmen
    - abhängig davon, ob Array sortiert oder unsortiert ist
    - lineares Durchlaufen bei unsortierten Arrays
    - Intervall-Teilung bei sortierten Arrays
  - falls Zahl nicht in Array enthalten, -1 zurückliefern

## Sequentielle/ Lineare Suche

...wird bei der Suche von Informationen in unsortierten Arrays angewendet.

- Problem: gegeben ist Folge von (a1, .... , an);
  - Array k-mal durchlaufen, bis gesuchtes Element gefunden oder kein Treffer (return -1)

| Fall          | Szenario | Aufwand |
|---------------|----------|---------|
| Günstigster   | k = 1    | O(1)    |
| Ungünstigster | k = n    | O(n)    |
| Mittlerer     | k = n/2  | O(n)    |

- Prinzip
  1. Übergabe Array mit Elementen und gesuchtem Element
  2. Durchlaufe Array bis gesuchtes Element gefunden wurde
  3. Sobald gesuchtes Element gefunden wurde, gebe dieses aus
  4. Sollte Element nicht in Array vorhanden sein, gebe -1 bzw. Fehlerbenachrichtigung aus

- Beispiel-Pseudocode
  1. Übergabe Array _zahlen_ mit Zahlen und Übergabe gesuchter Zahl
  2. i = 0
  3. Durchlaufe Array solange _zahlen_[i] != gesucht, i++
  4. Sobald zahlen[i] == gesucht, Rückgabe i

## Binäre Suche für sortierte Zahlen-Arrays

...funktioniert nach dem Prinzip der Intervall-Teilung für in sortierten Array gespeicherten Daten.

- Bedingungen
  - sortiertes Array
  - Array beinhaltet Zahlen

1. Falls das Array leer ist, gib -1 zurück
2. Falls das Array nicht leer ist, nimm das mittlere Element des Arrays
3. Falls sein Wert der gesuchte Wert ist, gib den Index des mittleren Elements zurück
4. Falls sein Wert kleiner als der gesuchte Wert ist, suche im rechten Teilarray weiter
5. FAlls sein Wert größer als der gesuchte Wert ist, suche im linken Teilarray weiter

- Zahlen-Array wird also in Teilarrays geteilt
- die zu untersuchenden Teilarrays werden durch zwei Indizes "von" und "bis" als Abschnitt des gesamten Arrays gekennzeichnet
- Teilarrays werden nach gleichen Prinzip wie gesamte Array am Anfang abgesucht
  - mittleres Element bestimmen
  - je nachdem, ob gleich/größer/kleiner Index zurückgeben/in rechten Teilarray/in linken Teilarray weitersuchen/-teilen

- Aufwand: O(log2(n))

## Vergleich Lineare- und Binäre Suche

- Binäre Suche effizienter
  - vor allem viel effizienter für große Datenmengen
  - verdoppelt sich zu durchsuchende Datenmenge, so verdoppelt sich der Aufwand bei der linearen Suche, wohingegen lediglich eine einzige zusätzliche Vergleichsoperation bei der binären Suchen notwendig ist
- Binäre Suche jedoch mit Anforderungen verbunden, was bei der linearen Suche nicht der Fall ist
  - alle Elemente in Liste in Positionen gespeichert
  - über diese Positionen lässt sich direkt auf die dort befindlichen Elemente zugreifen
  - auf Elementen ist Ordnung definiert (<=)
  - Elemente sind entsprechend dieser Ordnung platziert

## Zusammenfassung

- zwei Möglichkeiten Element in Array zu finden
  - lineares Durchlaufen -> Sequentielle/ Lineare Suche
  - Intervall-Teilung -> Binäre Suche
- Sequentielle/ Lineare Suche
  - Array von Anfang beginnend durchlaufen, bis Element gefunden oder keine weiteren Elemente in Array mehr vorhanden sind
- Binäre Suche
  - Bedingung: (aufsteigend) sortiertes Zahlenarray
  - Prinzip: Suche anhand des mittleren Elements des Arrays beginnen und durchführen
- Binäre Suche effizienter
  - verdoppelt sich zu durchsuchende Datenmenge, so verdoppelt sich nicht der Aufwand wie bei der linearen Suche, sondern es wird lediglich eine einzige zusätzliche Vergleichsoperation benötigt
- Binäre Suche jedoch Anforderungen
  - Zugriff über Positionen
    - alle Elemente in Positionen gespeichert
    - über diese Positionen direkt Zugriff auf dort befindliches Element
  - Anordnung Elemente nach Ordnung
    - Ordnung auf Elementen definiert (<=)
    - Elemente entsprechend der Ordnung angeordnet