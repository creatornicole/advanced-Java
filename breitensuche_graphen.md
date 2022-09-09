# Breitensuche in Graphen

...stellt eine Möglichkeit für das systematische Traversieren eines Baums/Graphen dar.

- durchsucht Baum/Graph zuerst in Breite
  - d.h. zuerst werden Nachfolgerknoten von Knoten v untersucht, bevor Zweige in Tiefe weiter betrachtet werden

## Algorithmus

1. Füge Startknoten s in eine First-In-First-Out-Warteschlange (FIFO-Warteschlange) ein
2. Markiere Startknoten s als besucht
3. Wiederhole bis Warteschlange leer ist
   - entferne den am längsten wartenden Knoten v
   - füge alle von v bislang noch nicht besuchten Knoten der Warteschlange hinzu
   - markiere diese als bereits besucht

## Behauptung

In jedem Graphen G ist es mittels Breitensuche möglich, jeweils den kürzesten Pfad von einem Knoten s zu allen anderen Knoten in proportionaler Zeit (E+V) zu finden.\
-> Dijkstra-Algorithmus

## Zusammenfassung

- Breitensuche durchsucht Baum/Graph zuerst in Breite, bevor Zweige der Nachfolgerknoten in ihrer Tiefe betrachtet werden
- Prinzip
  - Startknoten s wird zu FIFO-Warteschlange hinzugefügt und als besucht markiert
  - alle Nachbarknoten von s werden nun ebenfalls wieder zu FIFO-Warteschlange hinzugefügt und als besucht markiert
  - am längsten wartenden Knoten aus Warteschlange entfernen und von dessen wieder Nachfolgerknoten in FIFO-Warteschlange hinzufügen
  - solange wiederholen, bis Warteschlange leer
- Behauptung
  - mit Breitensuche möglich kürzesten Pfad in einem gegebenen Graphen von Knoten s zu allen anderen Knoten in proportionaler Zeit zu finden
  - siehe Dijkstra-Algorithmus
