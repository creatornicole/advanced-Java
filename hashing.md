# Hashing

...aufteilen der gesamten Schlüsselmenge.

- Bestandteile des Hash-Verfahrens
  - "gute" Hash-Funktion
  - Strategie zur Auflösung von Kollisionen

## Begriffe

| Begriff                                  | Erklärung                                                  |
|------------------------------------------|------------------------------------------------------------|
| Hashing                                  | to hash = zerhacken, Aufteilen der gesamten Schlüsselmenge |
| Position eines Datenelements im Speicher | ergibt sich durch Berechnung direkt aus Schlüssel (Key)    |
| Datenstruktur                            | häufig lineares Array der Größe m (Hashing-Tabelle)        |
| Slots                                    | Einträge in Hashingtabelle                                 |
| Hashfunktion mit Schlüssel s = h(s)      | Hash-Wert/ Hash-Adresse des Schlüssels s                   |

## Prinzip

- Raum R ist Raum aller möglichen Schlüssel
- Menge S ist Menge von Schlüssel (Keys), die aktuell in Hash-Tabelle abgelegt sind, wobei |S| = n gilt
- in Praxis |S| << |R|

## Hashfunktion

...wird genutzt, um Schlüssel auf Slots der Hash-Tabelle abzubilden.

- Hash-Funktion h bildet Schlüssel aus R auf Slots einer Tabelle T[0...m-1] ab
- im Vergleich zu normalen Array
  - bei normalen Array: Schlüssel s in Slot A[s] abgebildet
  - bei Hash-Tabellen: Schlüssel s in Slot T[h(s)] abgebildet (= _s hashes to..._)

- _gute_ Hash-Funktion erzeugt auch bei hohen Belegungsfaktor nur wenig Kollisionen und ist effizient zu berechnen
- heißt _perfekt_, wenn für Menge von Schlüssel S keine Kollisionen S auftreten
  - kann nur _perfekt_ sein, wenn |S| <= m
  - bzw. wenn Belegungsfaktor n/m <= 1

- wird bspw. von HashSet genutzt, um Werte in Array einzuordnen.

Bsp.:\
gegeben:
- Hashfunktion h... h(x) = (x % 3) + (x % 4)
- Werte A = { 1, 2, 3, 4, 5, 6, 7 }

| Index | Wert |
|-------|------|
| 0     |      |
| 1     | 4    |
| 2     | 1, 6 |
| 3     | 3, 5 |
| 4     | 2, 7 |
| 5     |      |
| 6     |      |
| 7     |      |

Beobachtung:
- Kollisionen treten auf, d.h. Plätze in Array mehrmals belegt
Lösung:
- bessere Hashfunktion

## Kollisionen

...treten immer dann auf, wenn man ein neues Element einfügen möchte, dessen Slot bereits belegt ist.\

-> Kollisionen beheben bzw. von Anfang an verhindern: "gute" Hash-Funktion verwenden

## Zusammenfassung

- Hashing = aufteilen der gesamten Schlüsselmenge
- Hashfunktion wird genutzt, um Schlüssel auf Slots der Hash-Tabelle abzubilden
- verschiedene Qualitäten einer Hashfunktion vorhanden
  - _gut_ -> erzeugt auch bei hohen Belegungsfaktor nur wenig Kollisionen und ist effizient zu berechnen
  - _perfekt_ -> wenn für Menge von Schlüsseln S keine Kollisionen auftreten -> dafür: |S| <= m bzw. Belegungsfaktor n/m <= 1
