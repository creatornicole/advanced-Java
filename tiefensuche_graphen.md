# Tiefensuche in Graphen

...das Ziel der Tiefensuche in einem Graph ist, das systematische Traversieren (Durchlaufen) durch einen gegebenen Graphen.

## Anwendungsbereiche

...werfen immer die Frage auf: Wie kann man die Tiefensuche für diesen Anwendungsbereich am besten implementieren?

- finde alle Knoten, die mit einem bestimmten Knoten im Graphen verbunden sind
- finde Pfad zwischen zwei Knoten

## Datenstrukturen

...sollen erreichen, dass Knoten auf folgenden Art und Weise bei der Tiefensuche besucht werden:

- markiere aktuellen Knoten v als besucht
- besuche anschließend rekursiv alle noch nicht markierten Nachbarknoten von v

- dafür bieten sich folgenden Datenstrukturen an:
| Datenstruktur | Anwendung |
|---------------|-----------|
| Boolean-Array marked[] | hilft beim Markieren der besuchten Knoten |
| Integer-Array edgeTo[] | zeichnet Pfad auf                         |

- Hinweis: edgeTo[w] == v, meint Verbindung v -> w wurde benutzt, um w das erste Mal zu erreichen
  - anders ausdrückt: in Integer-Array edgeTo[] ist Index w Knoten, an Index w in Array wird Knoten v, über den man w das erste Mal erreicht hat, gespeichert
- edgeTo[] speichert alle Eltern-Kind Beziehung die zusammen die Kanten eines Baumes bilden

## Annahmen

- Tiefensuche markiert alle mit s verbundenen Knotne in proportionaler Zeit abhängig vom Grad aller Knoten + Zeit, die zum Initialisieren des _marked[]_ Feldes benötigt wird
- nach durchgeführten Tiefensuche kann man wiederum in konstanter Zeit überprüfen, ob zwischen s und v Pfad existiert
  - diesen Pfad in proportionaler Zeit zu seiner Länge ausgeben v-s

## Eigenschaften

- Korrektheit
  - wenn w markiert, dann verbunden mit Startknoten s
  - wenn w mit s verbunden, so auch w markiert
  - falls w noch unmarkiert, so betrachte letzte Kante auf Pfad von s zu w
- Laufzeit
  - jeder mit s verbundene Knoten wird genau einmal besucht

## Zusammenfassung

- Eigenschaften
  - Korrektheit: Knoten w markiert <=> Knoten w mit Startknoten s verbunden
