# Java-Collections-Framework

...definiert eine einheitliche Architektur zur Darstellung und Bearbeitung von Sammlungen.

- "Collection" lässt sich als Behälter (Container) zur Verwaltung von Objekten sehen
- Collection-Framework beinhaltet Interfaces, Implementierungen und Algorithmen

## Collection Beispiele

- Collection-Framework ermöglicht Umsetzung verschiedener Datenstrukturen
  - Stapel
  - Warteschlange
  - Wörterbücher
  - Mengen
  - Listen
  - Bäume
- durch verschiedene Collections, wie bspw
  - Arrays
  - Vector
  - Hashtable
- unterschiedliche Datenstrukturen werden unterschiedlich implementiert

## Vorteile

...mit Framework viele Aufgaben mit viel weniger Programm-Code erledigen.

Bsp.:
| Problem                                            | Lösung mit Framework                                    |
|----------------------------------------------------|---------------------------------------------------------|
| Alphabetisches Sortieren einer String-Liste        | Collections.sort(liste);                                |
| -||- ohne Unterscheidung Groß- und Kleinschreibung | Collections.sort(liste, String.CASE_INSENSITIVE_ORDER); |
| Ausgabe von Array-Elementen                        | System.out.println(Arrays.asList(a));                   |

## Überblick Interfaces

...beschreiben häufig verwendete abstrakte Datentypen.

Bsp.:
- Iterable
  - Collection
    - Set -> Sorted Set
    - List
    - Queue -> Dequeue
- Iterator
  - ListIterator
- Map
  - SortedMap

### Allgemeine
| Interfaces   | definiert Methode(n)...                                                                                               |
|--------------|-----------------------------------------------------------------------------------------------------------------------|
| Collection   | allgemeine für Behälter                                                                                               |
| List         | für Behälter mit Elementen in einer bestimmten Reihenfolge, auf die über ihre Positionsnummer zugegriffen werden kann |
| Set          | für Behälter ohne doppelte Elemente und ohne bestimmte Reihenfolge (Mengen im Sinn der Mathematik)                    |
| SortedSet    | für Mengen mit einer Ordnung der Elemente (definiert durch Comparable bzw. Comparator)                                |

### Zum Traversieren

...zum Durchlaufen.

| Interfaces   | definiert Methode(n) zum Traversieren...                |
|--------------|---------------------------------------------------------|
| Iterable     | durch iterator()-Methode Iterator zur Verfügung stellen |
| Iterator     | eines Behälters                                         |
| ListIterator | einer Liste in beide Richtungen                         |

### Für Warteschlange-Behälter
| Interfaces | definiert Methode(n) für Warteschlangen-Behälter...                                                                                 |
|------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Queue      | deren Elemente nach Regel eingefügt und nur von vorn entnommen werden kann                                                          |
| Deque      | deren Elemente an beiden Enden nach der LIFO-Regel ("Last In - Firs Out") eingefügt und entnommen werden, quasi zweiseitiger Stapel |

- Deque = Double-Ended Queue = "Deck"

### Für Abbildungs-Behälter
| Interfaces | definiert Methode(n) für Abbildungs-Behälter...                                                                                              |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Map        | in denen "Schlüssel-Wert-Paare" gespeichert werden können, wobei keine doppelten Schlüssel erlaubt sind (Abbildungen im Sinn der Mathematik) |
| SortedMap  | mit einer Ordnung für die Schlüssel-Elemente (definiert durch Comparable bzw. Comparator)                                                    |


## Standardimplementationen der Interfaces

## Interface Iterable<E>

## Optionale Methoden

...besitzen alle Interfaces des Collection-Frameworks und sind "optionale" Methoden zur Veränderung des Behälters, d.h. diese müssen nicht unterstützt werden.

- dann jedoch so implementieren, sodass UnsupportedOperationException geworfen wird

Bsp.: Implementierung einer nicht unterstützten Methode
```java
  public void remove() {
    throw new UnsupportedOperationException();
  }
```
