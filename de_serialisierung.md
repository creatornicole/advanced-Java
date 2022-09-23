# Serialisierung und Deserialisierung

...um Objekte über Laufzeit hinaus verwenden zu können.

- um Objekt in Java zu serialisieren: zu serialisierendes Objekt muss Interface "Serializable" implementieren

## Serialisierung

...ermöglicht es, Objekt zu speichern.

- Byte-Streamklasse ObjectOutputStream dafür nutzen
- zusätzlich BufferedOutputStream
- und FileOutputStream, um gelesene Daten in Datei zu speichern
- Objekt in ObjectOutputStream schreiben (writeObject())
- und zum Schluss flush()

-> siehe Beispiel unten

## Deserialisierung

...ermöglicht zuvor gespeichertes Objekt zu späteren Zeitpunkt wieder zu laden.

- Byte-Streamklasse ObjectInputStream dafür nutzen
- zusätzlich BufferedInputStream
- und FileInputStream, um Daten aus Datei zu lesen
- Objekt aus Datei lesen mit readObject() und zu Objekt umwandeln nicht vergessen
- ausgelesenes Objekt in Variable speichern, sodass damit gearbeitet werden kann
- dann lässt sich schon auf Objekt der Klasse wie gewohnt zugreifen und damit arbeiten

## Beispiel der Serialisierung und Deserialisierung

Bsp.:
```java
/*
* Klasse von zu serialisierenden Objekt
*/

public class Schauspieler implements Serializable {

  private String name;
  private String vorname;
  private int alter;

  public Schauspieler(String name, String vorname, int alter) {
    this.name = name;
    this.vorname = vorname;
    this.alter = alter;
  }

  public String getName() {
    return name;
  }

  public String getVorname() {
    return vorname;
  }

  public int getAlter() {
    return alter;
  }
}
```

```java
/*
* Serialisierung
*/

public class Seri {
  public static void main(String[] args) {
    Schauspieler sch = new Schauspieler("McGregor", "Ewan", 51);
    ObjectOutputStream oos = null;
    try {
      oos = new ObjectOutputStream(new BufferedOutputStream(new FileOutputStream("Pfad zu Datei")));
      oos.writeObject(sch);
      oos.flush();
    } catch(IOException e) {
        e.printStackTrace();
    } finally {
      try {
        oos.close();
      } catch(Exception ex) {
        ex.printStackTrace();
      }
    }
  }
}
```

```java
/*
* Deserialisierung
*/

public class Deseri {
  public static void main(String[] args) {
    ObjectInputStream ois = null;
    try {
      ois = new ObjectInputStream(new BufferedInputStream(new FileInputStream("Pfad zu Datei")));
      Schauspieler sch = (Schauspieler) ois.readObject();
      System.out.println(sch.getVorname());
      System.out.println(sch.getName());
      System.out.println(sch.getAlter());
    } catch(IOException ioe) {
        ioe.printStackTrace();
    } catch(ClassNotFoundException cnfe) {
        cnfe.printStackTrace();
    } catch(Exception ex) {
        ex.printStackTrace();
    } finally {
        try {
          ois.close();
        } catch(Exception e) {
          e.printStackTrace();
        }
    }
  }
}
```

## Zusammenfassung

- um Objekte über Laufzeit hinaus verwenden zu können
- Serialisierung ermöglicht Objekte zu speichern
- Deserialisierung ermöglicht zuvor gespeichertes Objekt zu späteren Zeitpunkt wieder zu laden
- für Serialisierung Verschachtelung von Streams mit Byte-Streamklassen
  - ObjectOutputStream -> Serialisierung
    - flush() nicht vergessen
  - ObjectInputStream -> Deserialisierung
    - Speicherung in Variable nicht vergessen, um auf Objekt zuzugreifen und damit zu arbeiten
