# Algorithmus von Prim

...dient der Ermittlung des Minimum Spanning Tree (MST).

- Reminder: MST = Ein minimaler Spannbaum ist ein aufspannender Baum eines zusammenhängenden, ungerichteten Graphen.
Dieser verbindet alle Knoten mit minimaler Gesamtgewichtung für seine Kanten
- Voraussetzungen
  - zusammenhängender Graph
  - ungerichteter Graph
  - gewichtete Kanten

## Grundprinzip

- neuer Graph wird erstellt
- auf Grundlage eines beliebig ausgewählten Startknotens des alten Graphen MST bilden
- von aktuellen Knoten nächsten Knoten nehmen, welcher mit geringsten Kosten erreichbar ist

## Algorithmus

1. Beliebigen Knoten aus Graphen nehmen = Startknoten
2. Alle Kanten, die von aktiven Knoten erreichbar sind, in Betrachtung ziehen
3. Aus allen zurzeit betrachteten Kanten, Kante mit geringsten Gewicht nehmen und zu Knoten übergehen
3. Solange 2. und 3. durchführen, bis neue Graph alle Knoten des alten Graphen enthält

## Hinweise

- Prim-Algorithmus wählt immer nur aktuell beste Möglichkeit aus und betrachte nicht die global beste
  - zählt deswegen zu Greedy-Algorithmen (spezielle Klasse von Algorithmen in der Informatik)
  - Greedy-Algorithmus = wählt schrittweise Folgezustand aus, der zum Zeitpunkt der Wahl den größten Gewinn/beste Ergebnis verspricht.
  - Greedy-Algorithmen oftmals schnell, lösen Probleme aber nicht optimal

## Zusammenfassung

- MST wird beim Prim-Algorithmus gefunden, indem...
  - beliebiger Startknoten aus Graphen genommen wird
  - alle Kanten, die von aktiven Knoten erreichbar sind, in Betrachtung gezogen werden
  - die Kante aller gerade betrachteten Kanten ausgewählt wird, die das geringste Kantengewicht besitzt
