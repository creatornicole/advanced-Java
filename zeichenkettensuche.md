# Zeichenkettensuche

...umfasst die Suche in Texten.

- zu grunde liegenden Datentyp: String

- Texte lassen sich als Folge von Zeichenketten verstehen.
- Zeichenketten dabei als beliebige Aneinanderreihung beliebig vieler Zeichen aus endlichen Alphabet.
- Alphabet sind wiederrum Buchstaben und/oder Zeichen und/oder zahlreiche Sonderzeichen

- Voraussetzung Zeichenkette bei Textsuche:
  - nicht negative, ganzzahlige Länge
  - Zugriff auf i-te Zeichen einer Zeichenkette für jedes i >= 1 möglich

## Begriffe

| Begriff | Erklärung |
|---------|---------------------------|
| Text              | Folge von Zeichenketten |
| Zeichenkette      | beliebige Aneinanderreihung beliebig vieler Zeichen aus einem endlichen Alphabet |
| String processing | Algorithmen zur Verarbeitung von Zeichenketten |

- verschiedene Algorithmenarten zur Zeichenkettenverarbeitung:
  - Suche in Texten bzw. Erkennen bestimmter Muster (pattern matching)
  - Verschlüsseln, komprimieren von Texten
  - Analyse von Texten
  - Übersetzen von Texten

## Suchproblem

...kann bei der Suche in Texten wie folgt formuliert werden:

- Gegeben:
  - Text als Zeichenkette a1...aN
  - Zeichenkette bestehend aus Zeichen aus endlichen Alphabet
  - Muster als Zeichenkette b1...bM (mit bi Element des endlichen Alphabets und 1<= i <= M)

- Gesucht:
  - ein oder alle Vorkommen von b1...bM in a1...aN
  - d.h. Indizes i mit 1 <= i <= (N - M + 1)
  - und ai = b1 mit ai+1 = b2, ... , ai+M-1 = bM

- i.d.R. Länge N des Textes viel größer als Länge M des Musters

## Textarten

- statischer Text
  - Änderungen verhältnismäßig selten
  - Änderungen im Verhältnis zum Gesamtumfang geringfügig
  - Bsp.: Wörterbuch
- dynamischer Text
  - Änderungen verhältnismäßig häufig
  - Änderungen im Verhältnis zum Gesamtumfang erheblich
  - Bsp.: Texteditoren

## Suche in dynamischen Text

- bei der Suche in dynamischen Texten kann es sich lohnen, Suchalgorithmen von zwei Dingen abhängig zu machen:
  - Struktur des Musters
  - zu Grunde liegende Alphabet

- Suchalgorithmen zur Suche in dynamischen Text:
  - Naive Verfahren
  - Knuth-Morris-Pratt (KMP)
  - Boyer-Moore

## Naive Verfahren zur Textsuche

...sucht Muster in Text, indem man das Muster, beginnend beim ersten Zeichen des Textes, der Reihe nach an jeden Teilstring des Texte (mit Länge M) legt und zeichenweise von links nach rechts vergleicht.
Entweder findet man so eine Übereinstimmung oder es kommt zu einem sogenannten Mismatch.

- sucht Muster solange in Text, bis Vorkommen des Musters in Text gefunden wurde oder das Ende des Textes erreicht wurde
- Muster (N - M + 1)-mal an Text anlegen und jeweils ganz durchlaufen
  - daraus ergibt sich Anzahl der Vergleiche
  - Anzahl der Vergleiche: (N - M + 1) * M
- Laufzeit: O(N * M)
- naive Verfahren ist gedächtnislos
  - d.h. selbe Textstelle wird unter Umständen mehrfach inspiziert
  - d.h. Verfahren merkt sich nicht, welche Zeichen im Text bereits mit Anfangsstück des Musters übereinstimmte bis Mismatch auftrat

- Verbesserungsmöglichkeit: Muster bei Vergleich nicht komplett, sondern nur bis zu ersten Mismatch durchlaufen
  - Anzahl der Vergleiche verändert sich zu: O(M + N)

## Knuth-Morris-Pratt (KMP)

...unterscheidet sich zum naiven Verfahren in der Hinsicht, dass der Zeiger i auf die nächste zu vergleichende Textstelle gesetzt werden kann ohne diesen jemals zurückzusetzen.
Dies geschieht, indem die Kenntnis über der Zeichen, im Muster, die mit den darüber stehenden Zeichen im Text übereingestimmt haben, bis ein Mismatch auftrat, bekannt ist.

- Idee:
  - Mismatch bei Vergleich Muster mit Text an j-ten Stelle
  - so j-1 Zeichen zuvor übereingestimmt
  - diese Info nutzen, um Muster soweit wie möglich nach rechts zu verschieben
  - dabei darauf achten, dass kein Vorkommen im Text übersehen wird

- Grundlegend: Erste Zeichen des Musters an Stelle, an der Mismatch auftrat, setzen
  - Ausnahme: in zuvor durchgegangenen Substring befindet sich bereits Anfang des Musters, dann

- Umsetzung
  - mit Verschiebungstabelle
  - bevor Vergleich begonnen wird, muss Verschiebungstabelle aufgestellt werden
  - Grundprinzip der Verschiebungstabelle: Notieren an welcher Stelle (Index) in Muster, Zeichen bereits aufgetreten ist
  - nach Aufstellen der Verschiebungstabelle kann Vergleich begonnen werden
  - für Vergleich: jedes Zeichen des Musters mit an jeweils gerade befindlichen Zeichen des Textes vergleichen, bis Mismatch auftritt
  - bei Auftritt Mismatch, Muster je nach in Verschiebungstabelle befindlichen Faktor nach rechts verschieben (Aufpassen: by default schon immer 1 nach rechts, dass heißt Verschiebungsfaktor + 1 Positionen nach rechts)
  - erneut vergleichen und immer so weiter

Bsp.:

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster | a | b | a | b | d |   |   |   |   |   |   |   |   |

Zugehörige Verschiebungstabelle:
| Index        | 0  | 1 | 2 | 3 | 4 | 5 | -> Länge des Musters |
|--------------|----|---|---|---|---|---|----------------------|
| Muster       |    | a | b | a | b | d |                      |
| Verschiebung | -1 | 0 | 0 | 1 | 2 | 0 |                      |

- -1 = Symbol für keine Verschiebung
- 0 = Zeichen kommt zuvor in Muster noch nicht vor
- 1 = Zeichen kommt zuvor in Muster an Index 1 vor
- 2 = Zeichen kommt zuvor in Muster an Index 2 vor

Vergleich anfangen
| Text   | a | b | a | b | **c** | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|-------|---|---|---|---|---|---|---|---|
| Muster | a | b | a | b | **d** |   |   |   |   |   |   |   |   |

-> Mismatch tritt bei Vergleicht c mit d auf
-> Mismatch also bei Index 4
-> Laut Verschiebungstabelle erfolgt nun eine Verschiebung von 2 Stellen
-> daraus ergibt sich:

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster |   |   |   | a | b | a | b | d |   |   |   |   |   |

-> Mismatch tritt bereits bei Vergleich b mit a auf
-> Mismatch also bereits an Index 0
-> Verschiebungsindex = -1, d.h. 1 nach rechts (_1 Feld nach rechts ist immer dazu zu rechnen_)
-> daraus ergibt sich:

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster |   |   |   |   | a | b | a | b | d |   |   |   |   |

-> Mismatch tritt bereits bei Vergleich b mit a auf
-> Mismatch also bereits an Index 0
-> Verschiebungsindex = -1, d.h. 1 nach rechts
-> daraus ergibt sich:

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster |   |   |   |   |   | a | b | a | b | d |   |   |   |

-> Mismatch tritt bei Vergleich c mit a auf
-> Mismatch also an Index 3
-> Verschiebungsindex an Index 3 gleich 1
-> daraus ergibt sich:

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster |   |   |   |   |   |   |   | a | b | a | b | d |   |

-> Mismatch tritt bereits bei Vergleich c mit a auf
-> Mismatch also bereits an Index 0
-> Verschiebungsindex = -1, d.h. 1 nach rechts
-> daraus ergibt sich:

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster |   |   |   |   |   |   |   |   | a | b | a | b | d |

-> Muster stimmt mit Textabschnitt überein

## Boyer-Moore

... unterscheidet sich von den bereits vorgestellten dynamischen Suchalgorithmen vor allem in dem Aspekt der Vergleichsrichtung des Musters mit dem aktuellen Textabschnitt.

- Vergleich Zeichen Muster mit Zeichen im Text anders als bis jetzt bekannt von rechts nach links
  - d.h. Vergleich Muster mit Text beginnt immer beim letzten Zeichen des Musters
- dennoch Legen des Musters an Text von links nach rechts

- bei Mismatch: Berechnung der Verschiebung des Musters
  - Verschiebung von Zeichen abhängig machen, welches Mismatch zu verantworten hat (Vorkommen-Heuristik)
  - tritt Zeichen an Position, an der Mismatch aufgetreten ist, nicht im Muster auf so um durchlaufene Zeichen nach rechts verschieben
  - wenn Zeichen an Position, an der Mismatch aufgetreten ist, in Muster auftritt, so Muster soweit nach rechts verschieben, bis übereinstimmende Zeichen untereinanderstehen

Bsp.:

| e | r |   | s | a | g | t | e |   | a | b | r | a | k | a | d | a | b | r | a | , | a | b | e | r |   | n | i | c | h | t | s |   | g | e | s | c | h | a | h | . |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| a | b | e | r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   | a | b | e | r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   | a | b | e | r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   | a | b | e | r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   | a | b | e | r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   | a | b | e | r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   | a | b | e | r |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |


- mit diesem Verfahren oftmals möglich, Muster große Distanzen nach rechts zu verschieben
  - somit nur einen Bruchteil der Textzeichen des Textes mit Muster vergleichen nötig
  - dennoch kein Vorkommen des Musters in Text übersehen

## Bad Match Suche

1. Aufstellen der Bad Match Tabelle
   - bestimme Maximum aus 1 und (Länge des Musters - aktueller Index - 1)
   - für jedes Zeichen in Muster durchgehen
   - tritt Zeichen in Muster mehrmals auf, so geringeres Maximum in Bad Match Tabelle eintragen
2. Muster von links beginnend an Text legen
3. Zeichenweise von rechts nach links durchgehen
4. Tritt Mismatch auf, so Zeichen aus Text, welches Mismatch verursacht hat, in Bad Match Tabelle suchen und um angegebene Stellen nach rechts verschieben
   - tritt Zeichen aus Text, welches Mismatch verursacht hat, nicht in Bad Match Tabelle auf, so eingetragenen Index unter "*" als Verschiebungsfaktor nehmen

Bsp.:\
gegeben:
- Text... a b a b c a b c a b a b d
- Muster... a b a b d

1. Aufstellen Bad Match Tabelle
| Index  | 0 | 1 | 2 | 3 | 4 |
|--------|---|---|---|---|---|
| Muster | a | b | a | b | d |

- Maximum aus 1 und (Länge des Musters - aktueller Index - 1)
  - a... Max(1, 5 - 0 -1) = Max(1, 4) = 4
  - b... Max(1, 5 - 1 - 1) = Max(1, 3) = 3
  - a... Max(1, 5 - 2 - 1) = Max(1, 2) = 2
  - b... Max(1, 5 - 3 - 1) = Max(1, 1) = 1
  - d... Max(1, 5 - 4 - 1) = Max(1, 0) = 1
  - Sonstige(*)... Max(1, 5 - 0 - 1) = Max(1, 4) = 4 -> für sonstige Zeichen Index 0 nehmen

| Buchstabe | a | b | d | * |
|-----------|---|---|---|---|
| Index     | 2 | 1 | 1 | 4 |

2. Muster von links beginnend an Text legen
| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster | a | b | a | b | d |   |   |   |   |   |   |   |   |

3. Zeichenweise von links nach rechts durchgehen
4. Tritt Mismatch auf, so Zeichen aus Text, welches Mismatch verursacht hat, in Bad Match Tabelle suchen und um angegebene Stellen nach rechts verschieben

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster | a | b | a | b | d |   |   |   |   |   |   |   |   |

-> c verursacht Mismatch -> nicht in Bad Match Tabelle -> zählt unter Sonstige "*" -> Verschiebung um 4 nach rechts

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster |   |   |   |   | a | b | a | b | d |   |   |   |   |

-> a verursacht Mismatch -> in Bad Match Tabelle mit Verschiebung um 2 nach rechts gekennzeichnet

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster |   |   |   |   |   |   | a | b | a | b | d |   |   |

-> a verursacht erneut Mismatch -> Verschiebung erneut um 2 nach rechts

| Text   | a | b | a | b | c | a | b | c | a | b | a | b | d |
|--------|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Muster |   |   |   |   |   |   |   |   | a | b | a | b | d |

## Suche in statischen Texten

...kann von einer gewissen Vorarbeit profitieren. So geht mit dem Verfahren zuvor auch die Überlegung einher, wie man effizient Indizes konstruieren kann.

## Zusammenfassung

- Suchproblem
  - gegeben: Text, endliches Alphabet, Muster
  - gesucht: Muster im Text
- i.d.R. Text viel länger als Muster
- zwei Textarten
  - statisch -> Änderungen verhältnismäßig selten und geringfügig
  - dynamisch -> Änderungen verhältnismäßig häufig und erheblich
- Suchalgorithmen für Suche in dynamischen Texten
  - Naive Verfahren
    - Legen Muster an jeden Teilstring des Textes
    - Vergleich zeichenweise von links nach rechts
  - Knuth-Morris-Pratt (KMP)
    - berechnet mögliche Verschiebung des Musters nach rechts
    - basierend auf zuvor übereinstimmenden Zeichen
    - mit Verschiebungstabelle
  - Boyer-Moore
    - Anlegen Muster an Text erfolgt ebenso von links nach rechts
    - Vergleichsrichtung jedoch von rechts nach links
    - praktisch für kurze Zeichenfolge für viel Text -> mit Verfahren Muster oftmals um große Distanzen nach rechts verschieben möglich und somit nur einen Bruchteil der Textzeichen des Textes mit Muster vergleichen notwendig
  - Bad Match
    - Aufstellen Bad Match Tabelle
    - bei Mismatch, Zeichen aus Text, welches Mismatch verursacht hat, in Tabelle suchen und um eingetragenen Index (= Verschiebungsfakor) nach rechts verschieben
