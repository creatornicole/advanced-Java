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
| (siehe darüber) ohne Unterscheidung Groß- und Kleinschreibung | Collections.sort(liste, String.CASE_INSENSITIVE_ORDER); |
| Ausgabe von Array-Elementen                        | System.out.println(Arrays.asList(a));                   |

## Überblick Interfaces

...beschreiben häufig verwendete abstrakte Datentypen.

- Iterable
  - Collection
    - Set -> Sorted Set
    - List
    - Queue -> Dequeue



### Allgemeine
| Interfaces   | definiert Methode(n)...                                                                                               | Standardimplementationen        |
|--------------|-----------------------------------------------------------------------------------------------------------------------|---------------------------------|
| Collection   | allgemeine für Behälter                                                                                               |                                 |
| List         | für Behälter mit Elementen in einer bestimmten Reihenfolge, auf die über ihre Positionsnummer zugegriffen werden kann | ArrayList, LinkedList, (Vector) |
| Set          | für Behälter ohne doppelte Elemente und ohne bestimmte Reihenfolge (Mengen im Sinn der Mathematik)                    | HashSet, LinkedHashSet          |
| SortedSet    | für Mengen mit einer Ordnung der Elemente (definiert durch Comparable bzw. Comparator)                                | TreeSet                         |

- TreeSet und HashSet
  - Gemeinsamkeit: keine doppelten Werte bzw. Elemente
  - Unterschied: TreeSet speichert Werte nach Ordnung (natürlich oder künstlich), wohingegen HashSet Werte nach einer Hashfunktion speichert

### Zum Traversieren

...zum Durchlaufen.

- Iterator
  - ListIterator

| Interfaces   | definiert Methode(n) zum Traversieren...                |
|--------------|---------------------------------------------------------|
| Iterable     | durch iterator()-Methode Iterator zur Verfügung stellen |
| Iterator     | eines Behälters                                         |
| ListIterator | einer Liste in beide Richtungen                         |

### Für Warteschlange-Behälter
| Interfaces | definiert Methode(n) für Warteschlangen-Behälter...                                                                                 | Standardimplementationen  |
|------------|-------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| Queue      | deren Elemente nach Regel eingefügt und nur von vorn entnommen werden kann                                                          | LinkedList, PriorityQueue |
| Deque      | deren Elemente an beiden Enden nach der LIFO-Regel ("Last In - Firs Out") eingefügt und entnommen werden, quasi zweiseitiger Stapel | LinkedList, ArrayDeque    |

- Deque = Double-Ended Queue = "Deck"
- LinkedList als doppelt verkettete Ringliste realisiert

### Für Abbildungs-Behälter

- Map
  - SortedMap

| Interfaces | definiert Methode(n) für Abbildungs-Behälter...                                                                                              | Standardimplementationen            |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| Map        | in denen "Schlüssel-Wert-Paare" gespeichert werden können, wobei keine doppelten Schlüssel erlaubt sind (Abbildungen im Sinn der Mathematik) | HashMap, LinkedHashMap, (Hashtable) |
| SortedMap  | mit einer Ordnung für die Schlüssel-Elemente (definiert durch Comparable bzw. Comparator)                                                    | TreeMap                             |

- zu Map
  - Zuordnung Wert ("Schlüssel") zu Argument -> (Wert/Schlüssel, Argument)
  - Zuordnung Wert ("Schlüssel") zu mehreren Argumenten -> bspw. (Wert/Schlüssel, Set<Datentyp>)
    - typische Anwendungen für Maps solche Form sind Verzeichnisse aller Art wie Lexika, Wörterbücher, Telefon- oder Adressbücher

## Interface Iterable<E>

...stellt durch iterator()-Methode einen Iterator zur Verfügung.

- Iterator ermöglicht
  - einfachen Zugriff auf jedes Element einer Collection
  - darunterliegende Datenstruktur wird versteckt
- definiert Methoden zum Traversieren von Behältern

```java
//Iterator erstellen
public Interface Iterable<E> {
  Iterator<E> Iterator();
}

//Methoden zum Traversieren von Behältern
public Interface Iterator<E> {
  boolean hasNext();
  E next();
  void remove(); //optionale Methode, loescht zuletzt zurueckgegebenes Element
}
```

## Effiziente Suche mit Collection-Framework erreichen

...zielt darauf ab, möglichst schnell Elemente in einer Elementmenge zu finden (= Telefonbuchproblem).

- Datenstrukturen aus Collection-Framework, die dabei helfen
  - Hash-Table
  - Hash-Map
  - Dictionary
  - assoziative Arrays
- funktionieren nach Prinzip: Verallgemeinerung von Arrays

## Optionale Methoden

...besitzen alle Interfaces des Collection-Frameworks und sind "optionale" Methoden zur Veränderung des Behälters, d.h. diese müssen nicht unterstützt werden.

- dann jedoch so implementieren, sodass UnsupportedOperationException geworfen wird

Bsp.: Implementierung einer nicht unterstützten Methode
```java
  public void remove() {
    throw new UnsupportedOperationException();
  }
```

## Zusammenfassung

- Collection-Framework definiert eine einheitliche Architektur zur Darstellung und Bearbeitung von Sammlungen.
- Ermöglicht es Aufgaben mit viel weniger Programm-Code zu erledigen.
- Allgemeine Interfaces
  - List -> Elemente in Reihenfolge, Zugriff über Positionsnummer -> ArrayList, LinkedList
  - Set -> Mengen im Sinne der Mathematik (keine doppelten Elemente, ohne Reihenfolge) -> HashSet, LinkedHashSet
  - SortedSet -> Mengen mit Ordnung der Elemente -> TreeSet
- Zum Traversieren
  - Iterable -> iterator() -> stellt Iterator zur Verfügung
    - Iterator ermöglicht einfachen Zugriff auf jedes Element einer Collection
  - Iterator -> Behälter durchlaufen
  - ListIterator -> Liste in beide Richtungen durchlaufen
- Für Warteschlangen-Behälter
  - Queue -> einfügen nach bestimmter Regeln, entfernen nur von vorn -> LinkedList, PriorityQueue
  - Deque -> zweiseitiger Stapel, Elemente also von beiden Seiten entnehmbar -> LinkedList, ArrayDeque
- Für Abbildungs-Behälter
  - Map -> Abbildungen im Sinn der Mathematik ("Schlüssel-Wert-Paare" ohne doppelte Schlüssel) -> HashMap, LinkedHashMap
  - SortedMap -> Ordnung für Schlüssel-Elemente -> TreeMap
- optionale Methoden der Interfaces verlangen werfen von _UnsupportedOperationException_
