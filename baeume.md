# Bäume

...nichtlineare Datenstrukturen für flexibles und effizientes Einfügen, Löschen und Suchen.

- oft zur hierarchischen Verwaltung von Daten
- können aus ähnlichen Grundelementen wie verkettete Listen aufgebaut werden
- in der Informatik geht es im Allgemeinen um markierte Bäume (Bäume dessen Knoten Werte zugeordnet sind), in deren Knoten Daten bzw. Datenstrukturen enthalten sind

## Grundbegriffe

| Begriff                      | Erklärung                                                                                                   |
|------------------------------|-------------------------------------------------------------------------------------------------------------|
| Tiefe des Knotens            | auch Ebene oder Niveaus des Knotens ist Länge des Weges von der Wurzel zu einem Knoten (Wurzel hat Tiefe 0) |
| Höhe des Baumes              | größte Knoten-Tiefe eines Baumes                                                                            |
| Marke                        | Wert, der einem Knoten eines Baumes zugeordnet ist                                                          |
| Markierter Baum              | Baum dessen Knoten Werte zugeordnet sind                                                                    |
| Eltern-/Vater(knoten)        | Vorgängerknoten eines Knoten                                                                                |
| Kind(knoten)                 | Nachfolger-Knoten eines Knoten                                                                              |
| Pfad/ Weg                    | Kantenfolge (Länge des Pfades/des Weges ist Anzahl der Kanten bzw. Anzahl der Knoten - 1)                   |
| Teilbaum                     | auch Unterbaum heißt jeder Teil eines Baums, der selbst ein Baum ist                                        |
| Blatt                        | Knoten ohne Nachfolger                                                                                      |
| Innere Knoten                | alle Knoten, die keine Blätter sind (Knoten mit Nachfolgerknoten)                                           |

## Bäume als spezielle Graphen

- gerichtete Graphen bestehen aus Knoten und Kanten
  - jede Kante führt von einem Vorgängerknoten zu einem Nachfolgerknoten
- Bäume sind spezielle Graphen
  - haben einen speziellen Knoten: "Wurzel"
  - außer Wurzel hat jeder Knoten genau einen Vorgängerknoten
  - von der Wurzel aus führt zu jedem Knoten genau eine Kantenfolge

## Darstellungsmöglichkeiten

- zu speichernden Datenstrukturen durch Referenzen auf Nachfolgerknoten und/oder Vorgängerknoten ergänzt
  - Referenzen sind dabei die Kanten
  - analog zu Listen
- bei speziellen Baumstrukturen: Datenstrukturen in Arrays
  - dabei Indizes anstelle von Referenzen
  - Problem: variable Anzahl von Nachfolgerknoten erfordert im Allgemeinen Array von Referenzen
  - Ausweg: Darstellung mit zwei Referenzen: _linkes Kind_ und _rechte Geschwister_

## Traversierung

...systematisches Durchlaufen der Knoten.

Strategien
| Bezeichnung | Übersetzung | Prinzip                                                                        |
|-------------|-------------|--------------------------------------------------------------------------------|
| Pre-Order   | Vorordnung  | verarbeite Wurzel -> verarbeite linken Teilbaum -> verarbeite rechten Teilbaum |
| In-Order    | Inordnung   | verarbeite linken Teilbaum -> verarbeite Wurzel -> verarbeite rechten Teilbaum |
| Post-Order  | Nachordnung | verarbeite linken Teilbaum -> verarbeite rechten Teilbaum -> verarbeite Wurzel |

## Term-Bäume

...stellen Ausdrücke eindeutig dar, indem den Operatoren ihre Operanden explizit zugeordnet werden.

- Klammerung und Vorrang-Regeln werden durch Term-Bäume überflüssig

- Operatoren (Rechenzeichen) = Marke der inneren Knoten
- Operanden (Zahlen) zu Operator sind Teilbäume, die in Nachfolgerknoten (Kindknoten) beginnen
- Konstanten = Marke der Blätter

![Beispiel Term-Baum](termbaum.PNG)

## Binäre Bäume

...sind die am häufigsten verwendete Unterart der Bäume.

- Binärbaum kann zwei Form annehmen
  - leer
  - bestehend aus Wurzel mit linkem und rechtem Teilbaum, die wiederum Binärbäume sind
- alle Knoten nur maximal zwei direkte Nachkommen
  - Kindknoten lassen sich eindeutig in linkes und rechtes Kind einteilen
- Teilbaum leer? -> Kindknoten ist fehlend

## Binäre Suchbäume

...ein binärer Baum ist ein binärer Suchbaum, wenn für jeden Knoten gilt:

- Dateninhalte der Knoten seines linken Teilbaums sind alle kleiner als sein Dateninhalt
- Dateninhalt der Knoten seines rechten Teilbaums sind alle größer  oder gleich als sein Dateninhalt

- Einfügen: nach Prinzip eines binären Suchbaums einfügen
  - Marke des inneren Knoten kleiner -> linken Teilbaum weiter abgehen
  - Marke des innere Knoten größer/gleich -> rechten Teilbaum weiter abgehen
  - Größenvergleich solange durchführen, bis kein Nachfolgerknoten mehr existiert
  - an Stelle, an der kein Nachfolgerknoten mehr existiert, einfügen
- LÖschen: gelöschtes Element muss durch nächstkleineres Element ersetzt werden
  - wird Blatt gelöscht, so muss keine Veränderung vorgenommen werden, sondern es muss wirklich nur der Knoten mit dem Wert gelöscht werden
  - wird innerer Knoten gelöscht, so muss im rechten Teilbaum kleinste Element gesucht werden - dieses kleinste Element ersetzt zu löschenden Knoten
  - wird innerer Knoten gelöscht und exisitiert nur ein weiterer Teilbaum danach, so mit nächsten Wert des Teilbaums ersetzen
- Wurzel soll gelöscht werden, so unterscheidet man drei Fälle
  - linker Teilbaum leer: Wurzel ersetzen durch Wurzel des rechten Teilbaums
  - rechter Teilbaum leer: Wurzel ersetzen durch Wurzel des linken Teilbaums
  - beide Teilbäume nicht leer:
    - aus rechten Teilbaum Knoten mit minimalem Dateninhalt löschen, Dateninhalt in Wurzel übernehmen
    - aus linken Teilbaum Knoten mit maximalem Dateninhalt lösche, Dateninhalt in Wurzel übernehmen
- Suchen eines Wertes: ständiger "Größer-Kleiner-Gleich-Vergleich" mit Wurzel

## Zusammenfassung

- nichtlineare Datenstrukturen für flexibles und effizientes Einfügen, Löschen und Suchen
- am meisten in Informatik: Bäume dessen Knoten Werte in Form von Daten bzw. Datenstrukturen zugeordnet sind
- Darstellungsmöglichkeiten
  - analog zu Listen (zu speichernden Datenstrukturen durch Referenzen auf Nachfolgerknoten und/oder Vorgängerknoten ergänzen)
  - Array mit Indizes statt Referenzen (zwei Referenzen: linkes Kind und rechte Geschwister)
- Traversierungsstrategien
  - Pre-Order: Wurzel -> links -> rechts
  - In-Order: links -> Wurzel -> rechts
  - Post-Order: links -> rechts -> Wurzel
- Term-Bäume stellen mathematische Ausdrücke eindeutig dar, indem den Operatoren ihre Operanden explizit zugeordnet werden
- Binäre Suchbäume sind binäre Bäume, für dessen Knoten folgendes gilt...
  - Marke der Knoten des linken Teilbaums kleiner als Wurzel
  - Marke der Knoten des rechten Teilbaums größer/gleich Wurzel
