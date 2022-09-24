# advanced-Java

## Inhalt
1. Ein-/Ausgabe
   <details>
    <summary>Datei</summary>

    - Dateien wie Array auf Speichermedium
    - Zugriff durch Dateizeiger (file pointer), welcher sich um entsprechende Anzahl Bytes beim Lesen/Schreiben versetzt
    - Möglichkeiten Datei auslesen: Scanner Klasse

   </details>

   <details>
    <summary>Streams</summary>

    - Datenströme, über welche Datenaustausch erfolgt (abstrakes Konstrukt mit Fähigkeit Zeichen auf imaginäres Ausgabegerät zu schreiben und von diesem zu lesen)
    - Eingabestrom = InputStream = Reader
    - Ausgabestrom = OutputStream = Writer

    - Klassen für verschiedenartige Ströme
      - InputStream
      - OutputStream
      - Reader
      - Writer
    - Interfaces für bestimmte Funktionalitäten
      - DataInput
      - DataOutput
      - ObjectInput
      - ObjectOutput
      - Serializable
    - Dienstklassen für bestimmte Aufgaben
      - File
      - RandomAccessFile
    - Byte-Streamklassen zur Objektserialisierung
      - ObjectInputStream (Kindklassen: FileInputStream, ByteArrayInputStream)
      - ObjectOutputStream (Kindklassen: FileOutputStream)


   </details>

   <details>
    <summary>Exceptions</summary>

    - verschiedene IOExceptions beachten!
    - zwei Behandlungsmöglichkeiten
      - Abfangen durch try-catch-Anweisung
      - Weiterleiten durch throws-Deklaration

   </details>

   <details>
    <summary>NIO (New Input Output)</summary>

    - = New Input Output = Ersatz/Erweiterung für IO-Konzepte in Java durch Klassen unter java.nio.file
    - FileSystem
    - Path -> **zentrale Klasse**, repräsentiert Pfad/Datei in System, dadurch ganz einfaches kopieren/verschieben von Datei (auch von Webserver)
    - Files -> zur Verfügung stellen von Routineoperationen wie kopieren und löschen

   </details>
   <details>
    <summary>RAF</summary>

    = Random Access File
    - ermöglicht wahlfreien Zugriff auf Datei zur Ein- und Ausgabe
    - dafür Dateizeiger an entsprechende Position setzen
      - Dateizeiger Typ long
      - zeigt auf Byte, bei dem nächste Dateizugriff beginnt
      - Anfänge elementarer Datenelemente berechenbar
      - Anfänge anderer Datenelemente in extra Index-Datei speichern notwendig
      - getFilePointer() -> Abfrage aktuellen Dateizeigers
      - seek(long pos) -> Dateizeiger an angegebene Position setzen
    - implementiert Interfaces
      - DataInput -> read-Methoden
      - DataOutput -> write-Methoden
    - RAF nach Benutzung schließen

   </details>

   <details>
    <summary>URL und URLConnection</summary>

    - URL-Klasse repräsentiert Ressource im World Wide Web
    - URLConnection-Klasse besitzt Methoden, die einen von der Ressource der URL lesen und auf diesen schreiben lassen
    - Daten einer URL lesen
      - URL-Objekt des Webdokuments erstellen
      - Webdokument.openStream() (ist InputStream zum Auslesen)
      - Files.copy(InputStream in, Path target, CopyOptions option) (zum Kopieren aller Bytes eines InputStreams in Datei)

   </details>

   <details>
    <summary>De-/Serialisierung</summary>

    - um Objekte über Laufzeit hinaus verwenden zu können
    - zu serialisierendes Objekt muss Interface Serializable implementieren
    - Serialisierung ermöglicht Objekte zu speichern
    - Deserialisierung ermöglicht zuvor gespeichertes Objekt zu späteren Zeitpunkt wieder zu laden
    - für Serialisierung Verschachtelung von Streams mit Byte-Streamklassen
      - ObjectOutputStream -> Serialisierung
      - ObjectInputStream -> Deserialisierung

   </details>

2. Suchen/Sortieren
    <details>
     <summary>Suchen</summary>

     - beschränkt sich hier auf Zahlen-Arrays
     - zu lösendes Problem: in Zahlen-Array Index der vorgegebenen Zahl bestimmen
     - zwei Möglichkeiten
       - lineares Durchlaufen -> bei unsortierten Arrays -> Sequentielle/ Lineare Suche
       - Intervall-Teilung -> bei sortierten Arrays -> Binäre Suche

    </details>
    <details>
     <summary>Sortieren</summary>

     - Arrays aus einem oder keinem Element trivialerweise sortiert
     - Einfache Sortieralgorithmen
       - Prinzip: Array Nachbarelemente werden überprüft und gegebenenfalls vertauscht
       - Aufwand immer quadratisch (O(n^2))
       - Beispiele: Bubble-Sort, Selection-Sort, Insertion-Sort
     - Effiziente Sortieralgorithmen
       - Prinzip: "Teile und Herrsche"
       - Aufwand im ungünstigsten Fall: O(n*log2n)
       - Beispiele: Merge-Sort, Quick-Sort
     - Spezielle Sortierverfahren: Count-Sort, Radix-Sort

    </details>
    <details>
     <summary>Aufwand</summary>

     - zur Aufwandsbetrachtung wird Computer als "abstrakte Maschine" idealisiert, bei der alle Operationen die gleiche Zeiteinheit und alle elementaren Daten den gleichen Speicherplatz brauchen
     - Betrachtung von T(n) mit n -> unendlich
     - O-Notation soll dem Ziel dienen, eine möglichst einfache Klassifizierung des Aufwandes für unterschiedliche Algorithmen zu finden

    </details>
    <details>
     <summary>Zeichenkettensuche</summary>

     - Suchproblem
       - gegeben: endliches Alphabet, Text als Zeichenkette a1...an, Muster als Zeichenketten b1...bm
       - gesucht: Vorkommen Muster in Text, also b1...bm in a1...an
     - Suche in dynamischen Texten
       - Naive Verfahren -> einfach nacheinander Muster an Zeichenkette anlegen
       - Knuth-Morris-Pratt (KMP) -> mit Hilfe einer Verschiebungstabelle, die man zuvor anlegt, Suche durchführen
       - Boyer-Moore -> anlegen Muster an Text von links nach rechts, jedoch Vergleich von rechts nach links, Berechnung Verschiebung abhängig machen von Zeichen welches Mismatch zu verantworten hat (siehe "Regelungen" in extra Dok Zeichenkettensuche)
     - Suche in statischen Texten


    </details>

    <details>
     <summary>Dijkstra-Algorithmus</summary>

     - mit Wegsuche nach Dijkstra garantiert kostengünstigsten Weg in Graphen berechnen
     - Bedingungen:
       - gerichteter Graph
       - gewichteter Graph
       - Kantengewichte des Graphen sind nicht negativ
    - für jeden Knoten Kosten und Vorgänger festhalten
    - in jeder Iteration gegebenenfalls Kosten und Vorgänger der Nachfolger aktualisieren, wenn Kosten geringer sind, als bereits festgehalten
    - Nachfolger immer in Warteschlange hinzufügen
    - Durchgang solange durchführen, bis keine Nachfolger mehr in Warteschlange

    </details>

3. Datenstrukturen
    <details>
     <summary>Bibliotheken</summary>

     - erweitern Funktionalität von Java
     - qualitativ sehr unterschiedlich
     - Beispiele: Log4j, SLF4j, LogBack, JSON, JUnit, Apache Commons, Guava

    </details>
    <details>
     <summary>Collections-Framework</summary>

     - beinhaltet Interfaces, Implementierungen und Algorithmen zur einheitlichen Architektur, Darstellung und Bearbeitung von verschiedensten Behältern (also verschiedenster Datenstrukturen, die Dinge auf verschiedene Art und Weise einfügen und entnehmen lassen)
     - Bsp.: Collections.sort(), Arrays.asList()
     - Interfaces beschreiben häufig verwendete abstrakte Datentypen
       - Sammlungen (Mengen-Behälter)
         - Collection
         - List (ArrayList, LinkedList) -> Elemente in bestimmter Reihenfolge
         - Set (HashSet, LinkedHashSet) -> ohne bestimmte Reihenfolge, ohne Dopplung (Mengen im Sinn der Mathematik)
         - SortedSet (TreeSet) -> Mengen mit Ordnung (definiert durch Comparable/Comparator)
        - Zum Traversieren
          - Iterator -> Traversieren Behälter
          - ListIterator -> Traversieren Liste
        - Warteschlangen-Behälter
          - Queue (LinkedList, PriorityQueue) -> Entnahme nur von vorn
          - Deque (LinkedList, ArrayDeque) -> quasi zweiseitger Stapel (von beiden Enden Elemente nach LIFO ("Last-In-First-Out") einfügen und entnehmen möglich)
        - Abbildungs-Behälter
          - Map (HashMap, LinkedHashMap, Hashtable) -> Speicherung "Schlüssel-Wert-Paare", keine doppelten Schlüssel (Abbildungen im Sinn der Mathematik)
          - SortedMap (TreeMap) -> Ordnung auf Schlüssel

    </details>
    <details>
     <summary>Externe Datenstrukturen: XML, JSON</summary>

     - XML
       = extensible markup language (stark vereinfachte Markup Language)
       - dient Speicherung, Übertragung, Rekonstruktion von beliebigen Daten
       - Semantik -> Inhalt sehr flexibel wählbar
       - Syntax -> Grammatik sehr streng
       - Programmierschnittstellen: DOM, SAX, StAX, XLST, XPath
       - Anwendung: Websites, Grafiken, Web Services, Konfigurationen
     - JSON
       = JavaScript Object Notation
       - ähnlich zu XML jedoch kompakter
       - Anwendung: primär Webanwendungen, Apps

    </details>
    <details>
     <summary>Verkettete Listen</summary>

     - einfach verkettete lineare Liste
       - Aneinanderreihung von Listenelementen
       - Inhalt jedes Listenelements...
         - data -> Dateninhalt
         - next -> Verweis auf nächste Listenelement
       - Zugriff über erste Element
       - nur sequentielle Suche möglich
       - letzte Element an "leerem" Verweis erkennbar
       - wenn Verweis auf letzte Listenelement vorhanden, so Durchlaufen zum Einfügen nicht notwendig
     - Doppelt verkettete Ringliste -> mit erstem und letztem Hilfselement
       - Aneinanderreihung von Listenelementen
       - Inhalt jedes Listenelements...
         - data -> Dateninhalt
         - next -> Verweis auf nächste Listenelement
         - prev -> Verweis auf vorhergehende Listenelement
       - Eintrittselement _entry_ dient nicht zur Datenspeicherung
       - leere Liste wird durch Eintrittselement _entry_ mit Verweisen auf sich selbst dargestellt


    </details>
    <details>
     <summary>Hashing</summary>
    </details>

4. Bäume/Graphen

    <details>
     <summary>Graphen</summary>

     - bestehen aus Knotenmenge und Kantenmenge
     - Unterscheidung von gerichteter- und ungerichteter Graph
     - Darstellung unterschiedlich möglich
       - Kantenmenge -> Angabe Gesamtzahl Knoten, Angabe Gesamtzahl Kanten, zudem Angabe der Paarungen von Knoten, die verbunden sind
       - (Adjazenz)Matrix -> 2-dimensionales Knoten-zu-Knoten boolsches Feld bzw. Integer-Feld (Integer bei Gewichtung), Zeilen-/Spaltenanzahl = Anzahl der Knoten
       - Nachbarschaftsliste -> zu jedem Knoten existiert Liste von verbundenen Knoten

    </details>


    <details>
     <summary>Bäume</summary>

     - nichtlineare Datenstrukturen für flexibles und effizientes Einfügen, Löschen und Suchen
     - oft zur hierarchischen Verwaltung von Daten
     - Bäume sind spezielle Graphen
       - mit speziellen Knoten "Wurzel"
       - außer Wurzel hat jeder Knoten genau einen Vorgängerknoten
       - von Wurzel aus führt zu jedem Knoten genau eine Kantenfolge

     - Traversierung
       - Pre-Order: Wurzel -> linker Teilbaum -> rechter Teilbaum
       - In-Order: linker Teilbaum -> Wurzel -> rechter Teilbaum
       - Post-Order: linker Teilbaum -> rechter Teilbaum -> Wurzel

    </details>

    <details>
     <summary>MST = Minimum Spanning Tree</summary>

     - Teilgraph eines ungerichteten, gewichteten Graphen
     - Teilgraph enthält alle Knoten des Graphen mit minimalen Aufwand

    </details>

    <details>
     <summary>Termbäume</summary>

     - stellen (Rechen)Ausdrücke eindeutig dar
     - Eindeutig dadurch, dass Operatoren ihren Operanden explizit zugeordnet werden
     - Operatoren (also Rechenzeichen) = Marke der inneren Knoten
     - Operanden (Zahlen) zu Operator = Teilbäume, die in Nachfolger-/Kindknoten beginnen
     - Konstante = Marke der Blätter

    </details>

    <details>
     <summary>Binäre Bäume</summary>

     - all solche Bäume, derer Knoten maximal zwei direkte Nachfolger besitzen
     - Kindknoten lassen sich somit eindeutig in linkes und rechtes Kind einteilen

    </details>

    <details>
     <summary>Binäre Suchbäume</summary>

     - Binärer Baum ist Binärer Suchbaum, wenn gilt...
       - Marke der Knoten des linken Teilbaums sind alle kleiner als Marke des aktuellen Knotens
       - Marke der Knoten des rechten Teilbaums sind alle größer oder gleich der Marke des aktuellen Knotens
     - Einfügen und Suchen durch Größenvergleich
       - Größenvergleich bestimmt, welcher Teilbaum weiter abgegangen werden muss
       - Größenvergleich solange durchführen bis keine Nachfolgerknoten mehr existieren, an dieser Stelle einfügen
     - Löschen verlangt unterschiedliche Vorgehensweisen
       - Löschen eines Blattes -> einfach Blatt löschen
       - Löschen innerer Knoten mit zwei Teilbäumen -> kleinste Element des rechten Teilbaums ersetzt inneren Knoten
       - Löschen innerer Knoten mit einem Teilbaum -> innerer Knoten mit nächsten Wert des Teilbaums ersetzen
       - Löschen der Wurzel
         - linker Teilbaum leer: Wurzel ersetzen durch Wurzel des rechten Teilbaums
         - rechter Teilbaum leer: Wurzel ersetzen durch Wurzel des linken Teilbaums
         - beide Teilbäume nicht leer
           - aus rechten Teilbaum Knoten mit minimalsten Dateninhalt löschen, Dateninhalt in Wurzel übernehmen
           - aus linken Teilbaum Knoten mit maximalen Dateninhalt löschen, Dateninhalt in Wurzel übernehmen

    </details>


    <details>
     <summary>Tiefen-/Breitensuche in Graphen</summary>

     - Tiefensuche durchsucht zuerst in Tiefe
       - d.h. wird so weit wie möglich entlang jedes Zweigs untersucht
       - maximaler Speicherbedarf = Tiefe des Baumes
       - einsetzen wenn man weiß, dass...
         - Lösung irgendwo tief in einem Baum oder weit entfernt vom Quellscheitelpunk im Diagramm liegt
         - Baum sehr breit ist -> benötigt in diesem Fall weniger Speicher als bei Breitensuche

     - Breitensuche durchsucht zuerst in Breite
       - d.h. untersucht zuerst Nachbarknoten, bevor zu Nachbarn der nächsten Ebene übergangen wird
       - maximaler Speicherbedarf = Breite des Baumes
       - einsetzen wenn man weiß, dass...
         - Lösung nicht so weit vom Quellknoten entfernt liegt
         - Baum besonders tief -> benötigt in diesem Fall weniger Speicher als Tiefensuche




    </details>

## Wichtige Klassen zu Themenbereichen

- Scanner
- FileSystem
- Path
- Files
- File
- RandomAccessFile (implementiert DataInput und DataOutput)
- URL
- URLConnection
- InputStream
- OutputStream
- Reader
- Writer
- ObjectInputStream (Bsp.: FileInputStream)
- ObjectOutputStream (Bsp.: FileOutputStream)


## Wichtige Interfaces zu Themenbereichen

- DataInput
- DataOutput
- ObjectInput
- ObjectOutput
- Serializable
- Collection
- List (-> ArrayList, LinkedList)
- Set (-> HashSet, LinkedHashSet)
- SortedSet (-> TreeSet)
- Iterator
- ListIterator
- Queue (-> LinkedList, PriorityQueue)
- Deque (-> LinkedList, ArrayDeque)
- Map (-> HashMap, LinkedHashMap, Hashtable)
- SortedMap (-> TreeMap)

## Referenz

Hauptquelle: Modul 21061 Einführung in die Informatik ||: Weiterführende Programmierung gelehrt von Knut Altroggen an der Hochschule Mittweida
Abbildungen: ebd.
