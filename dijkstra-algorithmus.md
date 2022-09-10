# Wegsuche nach Dijkstra

...hilft dabei den kürzesten bzw. kostengünstigsten Weg in einem Graphen zu berechnen.\
Notizen basierend auf [Studyflix Beitrag](ht.tps://studyflix.de/informatik/dijkstra-algorithmus-1291)

- Behauptung: findet garantiert kürzesten Pfad zu Punkt w ausgehend von Startpunkt s
- Bedingungen
  - gerichteter Graph
  - gewichteter Graph
  - Kantengewichte des Graphen sind nicht negativ

## Begriffserläuterungen

| Begriff       | Erläuterung                                       |
|---------------|---------------------------------------------------|
| Kantengewicht | Kosten, um von einem Punkt zum nächsten zu kommen |

## Initialisierung

- Tabelle zum Überblick behalten anlegen
  - erste Spalte Iteration
  - jede weitere Spalte ist Knoten
    - für jeden Knoten Kosten angeben
    - für jeden Knoten direkten Vorgänger angeben
  - Kosten zum Startknoten ist Null (man ist ja schon zuhause)
  - zu möglichen Reiseorten ist Weg unbekannt -> Kosten erst einmal mit unendlich bewerten
    - nach und nach werden Kosten angepasst

- Warteschlange, in welcher alle Knoten, die bereits gefunden wurden, eingefügt werden
  - am Anfang nur Startknoten bekannt
  - Startknoten als erstes in Warteschlange einfügen

## Iteration 1

- in ersten Iteration ist in Warteschlange nur ein Element (Startknoten)
- direkte Nachfolger dieses Elements betrachten
- für direkte Nachfolger, Kosten, um dahin zu kommen und Element als Vorgänger in Tabelle tragen
- wenn alle Nachfolger betrachtet, betrachtete Element als besucht markieren
- alle Nachfolger in Warteschlange hinzufügen

## Iteration 2

- Knoten, den man mit geringsten Kosten erreicht aus Warteschlange nehmen
- von dessen Knoten die direkten Nachfolger betrachten
- hier auch wieder Kosten und Vorgänger für Nachfolger in Tabelle tragen
  - gegebenenfalls aktualisieren
  - darauf achten, dass Kantengewicht zu bisherigen Kosten dazu addiert wird
- Nachfolger, die noch nicht in Warteschlange sind in diese einfügen
- betrachteten Knoten als besucht markieren

## Interation 3-n

- erneut Knoten, den man mit geringsten Kosten erreicht, aus Warteschlange nehmen
- dessen Nachfolger betrachten
- Kosten und Vorgänger eintragen und gegebenenfalls aktualisieren
- Nachfolger, die noch nicht in Warteschlange sind, in diese einfügen
- gerade betrachteten Knoten als besucht markieren
- ...
- sobald keine weiteren Knoten mehr in die Warteschlange aufgenommen werden, sie also leer ist, wird der Algorithmus beendet

## Ablesen Weg aus Tabelle

- ablesen erfolgt rekursiv
- Bsp.: Knoten E erreicht man über Vorgänger C, diesen erreicht man am besten über B und dorthin kommt man direkt über den Startknoten A, somit ist der kürzeste Weg vom Startknoten A zu E über Knoten B und C

## Zusammenfassung

- Dijsktra-Algorithmus dient dazu, den kürzesten Weg ausgehend vom Startknoten zu beliebigen Knoten in Baum/Graph zu finden
- dafür: gerichteter Graph, gewichtet, Kantengewichte nicht negativ
- Durchführung
  - Tabelle anlegen
    - erste Spalte Iteration
    - jede weitere mit Knoten, für den jeweils Kosten und Vorgänger notiert werden
  - Warteschlange erstellen, in denen zu besuchende Knoten warten
  - im Allgemeinen Knoten aus Warteschlange mit geringsten Kosten nehmen
  - von diesem Knoten direkte Nachfolger betrachten und je nachdem Tabelle (Kosten und Vorgänger) aktualisieren (wenn besser)
  - solange durchführen, bis Warteschlange leer
