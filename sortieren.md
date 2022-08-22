# Sortieren

- Prinzip der Sortieralgorithmen


## Einfache Sortieralgorithmen

- Prinzip: Werden beim Überprüfen eines Arrays Nachbarelemente in falscher Reihenfolge gefunden, so werden sie vertauscht.

| Algorithmus    | Prinzip                                                                                                        | Aufwand              | Verbesserungsmöglichkeiten                                         |
|----------------|----------------------------------------------------------------------------------------------------------------|----------------------|--------------------------------------------------------------------|
| Bubble-Sort    | größte Element in Abschnitt an letzte Position in Abschnitt bringen                                            | O(n^2) = quadratisch | aufhören, wenn in einem Durchlauf keine Elemente getauscht wurden  |
| Selection-Sort | Sortieren durch Auswahl des i.kleinsten Elements für die Position i des Arrays                                 | O(n^2) = quadratisch |                                                                    |
| Insertion-Sort | Sortieren durch Einfügen des nächsten Elements in ein bereits sortiertes Teil-Array an der richtigen Stelle    | O(n^2) = quadratisch |                                                                    |

- Aufwand bei einfachen Sortieralgorithmen immer quadratisch, da im ungünstigsten Fall jedes Element mit jedem anderen verglichen wird.

## Bubble-Sort

1. 1. Durchlauf Array komplett durchlaufen, größte Element an letzte Position in Array verschieben
2. 2. Durchlauf: Array bis zum vorletzten Platz durchlaufen, davon größte (also in 2. Durchlauf zweitgrößte) Element an letzte Position in durchlaufenen Abschnitt (also in 2. Durchlauf an vorletzte Position) bringen
3. ...
4. (n-1). Durchlauf: Letzten beiden Element vergleichen und ggf. vertauschen

## Selection-Sort

...in jedem Schritt kleinste (größte) der noch ungeordneten Elemente suchen und am rechten Ende der bereits sortierten Elemente einordnen.

- ob größte oder kleinste Element suchen, ist davon abhängig, ob man diese auf- oder absteigend sortieren will
  - aufsteigend: kleinste Element suchen
  - absteigend: größte Element suchen

- [sortierter Bereich][unsortierter Bereich]
  -> k erste Position im noch unsortierten Bereich
  -> i Position des kleinsten/größten Elements im noch unsortierten Bereich
  -> Element an Stelle k mit Element an Stelle i tauschen
- un-/sortierter Bereich ändert sich pro Durchlauf
  - sortierter Bereich wird immer um ein Element größer
  - unsortierter Bereich wird immer um ein Element kleiner

## Insertion-Sort

## Effiziente Sortieralgorithmen
