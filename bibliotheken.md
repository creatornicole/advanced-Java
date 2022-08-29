# Bibliotheken

...erweitern Java's Funktionalität.

- Bibliotheken umfassen i.d.R. speziellen Bereich
  - Testen von Java Anwendungen
  - Grafische Anwendungen
  - (Fehler-)Berichterstattung
  - Abfrage von externen Quellen
    - Datenbanken
    - JSON

- Qualität schankt sehr, da keine genaue Richtlinien existieren

## Bibliotheken zum Logging von Fehlern

Bsp.:
- Log4j
- SLF4j
  - beliebteste Logging-Bibliothek
  - Simple Logging Facade for Java
  - ermöglicht zentrales Logging von Fehlern, Zuständen, ...
- LogBack

## Bibliothek zur JSON Verarbeitung

...die sonst nicht vorhanden wäre.

- schlankes Datenaustauschformat
- für Menschen besser lesbar, leichtgewichtig, erfordert weniger Programmieraufwand

Bsp.: Umsetzung mit Simple-JSON, **Unsaubere Umsetzung**
```java
  JSONObject obj = new JSONObject();
  obj.put("name", "Michael");
  obj.put("age", 27);
  obj.put("salary", 6000.0);
  System.out.print(obj);
  BufferedWriter lesen = new BufferedWriter(new FileWriter("res\\test.json"));
  lesen.write(obj.toJSONString());
  lesen.close();
```

## JUnit

... Framework zum Testen von Java Programmen.

- Berücksichtigung umfassender Akzeptanz- und Unit-Tests hat deutlich positiven Effekt auf Struktur der Software
  - da, um Modul/Anwendung testbar zu machen, diese geeignet entkoppelt sein muss
  - je testbarer, desto besser gekapselt (modularer)
  - hat verbesserte Auswirkungen auf Architektur und Design

- Beispiel-Testmethoden
  - assertTrue(Boole'sche Bedingung)
  - assertFalse(Boole'sche Bedingung)
  - asssertEquals(Soll-Wert, Ist-Wert)
  - assertEquals(Soll-Wert, Ist-Wert, delta)
    - mögliche Typen: double, float
  - assertNull(Objekt)
  - assertNotNull(Objekt)
  - assertSame(Objekt1, Objekt2);
  - assertNotSame(Objekt1, Objekt2);
  - fail()

## Apache Commons

...Java-Bibliothek die darauf abzielt, allgemein verwendbare Klassenbibliotheken (_reusable components_) für die Programmiersprache zur Verfügung zu stellen.

Bsp.: Grafische Darstellung von Funktionen/Abbildungen in Mathe
```java
  Line l1 = new Line(new Vector2D(0, 0), new Vector2D(1, 1), 0);
  Line l2 = new Line(new Vector2D(0, 1), new Vector2D(1, 1.5), 0);
  Vector2D intersection = l1.intersection(l2);
```

## Guava

...von Google entwickelt, dient der Erweiterung von Bibliotheken:

|                          | schnelle Methoden schreiben von... |
|--------------------------|------------------------------------|
| StringHelper             | toString()                         |
| ComparisonChain          | compareTo() inkl. Verkettung       |
| Mathematische Funktionen | bspw. GGT, BigInteger              |       


## Zusammenfassung

- Bibliotheken erweitern Funktionalität von Java.
- jede Bibliothek meist für einen speziellen Bereich
- beliebteste Logging-Bibliothek: SLF4j
