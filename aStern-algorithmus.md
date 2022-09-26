# A*-Algorithmus

...Algorithmus zum Finden des kürzesten/kostengünstigsten Pfades zwischen zwei Knoten in einem Graphen mit positiven Kantengewichten.

- Verallgemeinerung und Erweiterung des Dijkstra-Algorithmus

- Algorithmus ist vollständig und optimal, d.h. wenn optimale Lösung existiert, so wird diese auch gefunden

- Voraussetzungen
  - gerichteter Graph
  - gewichteter Graph
  - Kantengewichte positiv

## Prinzip

- untersucht die Knoten zuerst, die _wahrscheinlich_ schnell zum Ziel führen

## Ermittlung des wahrscheinlich besten Knotens

- alle bekannten Knoten x durch Metrix Wert f(x) zuordnen
- f(x) gibt Abschätzung an, wie lang der Pfad von Knoten x von Start zum Ziel im günstigsten Fall ist
- Knoten mit geringsten f-Wert wird als nächstes untersucht

f(x) = g(x) + h(x)\
wobei g(x)... bisherigen Kosten vom Startknoten aus\
und h(x)... geschätzten Kosten von x bis zu Zielknoten

- Hinweis: für besseres Verständnis siehe dafür handschriftliche Notizen

## Zusammenfassung

- Verallgemeinerung und Erweiterung des Dijkstra-Algorithmus
  - findet garantiert kürzesten Weg in gerichteten, positiv gewichteten Graphen zwischen zwei Knoten, wenn ein solcher existiert
- auswählen des nächsten Knotens, welcher am  vielversprechendsten scheint
  - dafür Berechnung
  - Berechnung stellt Abschätzung, wie lang Pfad von Knoten x zu Zielknoten im günstigsten Fall ist, dar
  - Knoten mit bester Abschätzung wird als nächstes untersucht
