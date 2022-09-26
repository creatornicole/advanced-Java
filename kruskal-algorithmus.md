# Kruskal Algorithmus

...dient der Ermittlung des Minimum Spanning Tree (MST).

- Reminder: MST = Ein minimaler Spannbaum ist ein aufspannender Baum eines zusammenhängenden, ungerichteten Graphen.
Dieser verbindet alle Knoten mit minimaler Gesamtgewichtung für seine Kanten
- Voraussetzungen
  - zusammenhängender Graph
  - ungerichteter Graph
  - gewichtete Kanten

## Grundprinzip

- Krukal Algorithmus findet Teilmenge der Kanten aus dem gegebenen Diagramm, die jedem im Diagramm befindlichen Knoten abdeckt.
- Dabei wird die Summe der Kantengewichte so gering wie möglich gehalten.

## Algorithmus

1. Alle Kanten des Graphen aufsteigend sortieren
2. Kanten nun nacheinander auswählen
3. Wenn kein Kreis durch Hinzufügen der jeweiligen Kante zum MST gebildet wird, wähle die Kante für den MST aus
4. Solange 2. und 3. wiederholen bis alle Kanten durchgegangen

## Zusammenfassung

- MST wird beim Kruskal-Algorithmus gefunden, indem...
  - Kanten aufsteigend nach ihren Gewichten sortiert werden
  - die sortierten Kanten nacheinander durchgegangen werden
  - die jeweilige Kante ausgewählt wird, wenn kein Kreis durch Hinzufügen dieser zum MST gebildet wird
