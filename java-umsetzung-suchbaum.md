# Beispielumsetzung eines Suchbaums in Java

Inhalt:
- zwei Klassen
  - Node -> Knoten in Baum
  - SuchBaum -> Baum an sich
- ohne grafische Darstellung
- dient beispielhaften Umsetzung folgender Logik
  - Aussage darüber treffen, ob Knoten in Baum vorhanden ist
  - neuen Knoten zu Baum hinzufügen (iterativ sowie rekursiv)
  - Knoten aus Baum löschen
  - minimalsten Wert eines Baumes ermitteln

```java

/*
 * Repraesentiert das einzelne Element im Suchbaum
 */

public class Node {

	private Node lchild; //linke (kleinere) Element des Knotens
	private Node rchild; //rechte (groessere) Element des Knotens
	private int key; //Wert des Knotens

	public Node(int key) {
		this.key = key;
		this.lchild = null;
		this.rchild = null;
	}

	/**
	 * Linke Element des Knotens erhalten
	 * @return linke Element des Knotens
	 */
	public Node getLchild() {
		return lchild;
	}

	/**
	 * Linke Element des Knotens (neu) setzen
	 * @param lchild
	 */
	public void setLchild(Node lchild) {
		this.lchild = lchild;
	}

	/**
	 * Rechte Element des Knotens erhalten
	 * @return rechte Element des Knotens
	 */
	public Node getRchild() {
		return rchild;
	}

	/**
	 * Rechte Element des Knotens (neu) setzen
	 * @param rchild
	 */
	public void setRchild(Node rchild) {
		this.rchild = rchild;
	}

	/**
	 * Wert des Knotens erhalten
	 * @return Wert des Knotens
	 */
	public int getKey() {
		return key;
	}

	/**
	 * Wert des Knotens (neu) setzen
	 * @param key
	 */
	public void setKey(int key) {
		this.key = key;
	}
}
```

```java
/*
 * Repraesentiert den Suchbaum
 */

public class SuchBaum {

	private Node root; //Wurzel des Suchbaums

	//Default Konstruktor
	public SuchBaum() {

	}

	//Erstellen Suchbaum mit Wurzel
	public SuchBaum(Node k) {
		root = k;
	}

	/**
	 * Gibt Wurzel des Suchbaums zurueck
	 * @return Wurzel des Suchbaums
	 */
	public Node getRoot() {
		return root;
	}

	/**
	 * Setze Wurzel des Suchbaums (neu)
	 * @param root
	 */
	public void setRoot(Node root) {
		this.root = root;
	}

	/**
	 * Rueckgabe Wahrheitswert, ob Knoten in Suchbaum existiert
	 * @param key gesuchte Wert
	 * @return true/false ob Knoten in Suchbaum existiert
	 */
	public boolean member(int key) {
		boolean erg = false; //solange false bis Wert gefunden
		//Baum durchlaufen
		Node knoten = root;
		//Suche solange Baum nicht zu Ende und Wert nicht gefunden
		while((knoten != null) && (erg == false)) {
			if(knoten.getKey() == key) { //Knoten ist gesuchter Wert
				erg = true;
			} else if(knoten.getKey() < key) { //Knotenwert kleiner -> rechten Teilbaum weiter durchsuchenTeilbaum
				knoten = knoten.getRchild();
			} else if(knoten.getKey() > key) { //Knotenwert groesser -> linken Teilbaum weiter durchsuchen
				knoten = knoten.getLchild();
			}
		}		
		return erg;
	}

	public boolean memberRekursiv(int key) {
		boolean erg = false;
		if(root.getKey() == key) {
			erg = true;
		} else {
			if(key < root.getKey()) {
				SuchBaum lTB = new SuchBaum(root.getLchild());
				lTB.memberRekursiv(key);
			} else {
				SuchBaum rTB = new SuchBaum(root.getRchild());
				rTB.memberRekursiv(key);
			}
		}
		return erg;
	}

	/**
	 * Rueckgabe Knoten
	 * @param key
	 * @return Knoten selbst oder null falls dieser Wert keinen Treffer ergibt
	 */
	public Node find(int key) {
		boolean gefunden = false; //solange false bis Wert gefunden
		//Baum durchlaufen
		Node knoten = root;
		Node gesuchterKnoten = null;
		//Suche solange Baum nicht zu Ende und Wert nicht gefunden
		while((knoten != null) && (gefunden == false)) {
			if(knoten.getKey() == key) {
				gesuchterKnoten = knoten;
			} else if(knoten.getKey() < key) { //Knotenwert kleiner -> rechten Teilbaum weiter durchsuchen
				knoten = knoten.getRchild();
			} else if(knoten.getKey() > key) {
				knoten = knoten.getLchild(); //Knotenwert groesser -> linken Teilbaum weiter durchsuchen
			}
		}
		return gesuchterKnoten;
	}

	public Node findRekursiv(int key) {
		Node gesucht = null;
		if(root.getKey() == key) {
			gesucht = root;
		} else {
			if(key < root.getKey()) {
				SuchBaum lTB = new SuchBaum(root.getLchild());
				lTB.findRekursiv(key);
			} else {
				SuchBaum rTB = new SuchBaum(root.getRchild());
				rTB.findRekursiv(key);
			}
		}
		return gesucht;
	}

	/**
	 * Hinzufuegen Knoten an richtiger Stelle in Suchbaum
	 * @param key
	 */
	public void insert(int key) {
		boolean continueSearching = true;
		//Wurzel leer -> Element wird Wurzel
		if(root == null) {
			root = new Node(key);
		} else { //Wurzel nicht leer
			Node aktuelles = root;
			while(continueSearching) {
				//abwaegen ob groesser oder kleiner
				if(key < aktuelles.getKey()) { //key kleiner als aktueller Wert des Nodes
					if(aktuelles.getLchild() == null) {
						aktuelles.setLchild(new Node(key));
						continueSearching = false;
					} else {
						aktuelles = aktuelles.getLchild();
					}
				} else { //key groesser als aktueller Wert des Nodes
					if(aktuelles.getRchild() == null) {
						aktuelles.setRchild(new Node(key));
						continueSearching = false;
					} else {
						aktuelles = aktuelles.getRchild();
					}
				}
			}
		}
	}

	public void insertRekursiv(int key) {
		if(root == null) {
			root = new Node(key);
		} else {
			if(key == root.getKey()) {
				System.out.println("Wert existiert in Baum bereits.");
			} else {
				if(key < root.getKey()) {
					SuchBaum lTB = new SuchBaum(root.getLchild());
					lTB.insertRekursiv(key);
					root.setLchild(lTB.getRoot()); //erreicht Verknuepfung
				} else {
					SuchBaum rTB = new SuchBaum(root.getRchild());
					rTB.insertRekursiv(key);
					root.setRchild(rTB.getRoot()); //erreicht Verknuepfung
				}
			}
		}
	}

	/**
	 * Loescht Wert aus Suchbaum
	 * @param key
	 */
	public void delete(int key) {
		if(member(key)) {
			if(key == root.getKey()) {
				//Beachten dreier Regeln

				if(!((root.getLchild() == null) && (root.getRchild() == null))) { //wenn mind ein Teilbaum vorhanden
					if(root.getLchild() == null) {
						//1: linker Teilbaum leer: Wurzel ersetzen durch Wurzel des rechten Teilbaums
						root = root.getRchild();
					} else if(root.getRchild() == null) {
						//2: rechter Teilbaum leer: Wurzel ersetzen durch Wurzel des linken Teilbaums
						root = root.getLchild();
					} else { //kein Teilbaum leer
						//3: beide Teilbaeume nicht leer: aus rechten Teilbaum Knoten mit minimalem Dateninhalt loeschen, Dateninhalt als Wurzel uebernehmen
						//3: analog dazu: loeschen Maximums aus linken Teilbaum und Dateninhalt als Wurzel setzen

						//Knoten mit minimalsten Dateninhalt aus rechten Teilbaum loeschen
						//minimalsten Wert aus rechten Teilbaum herausfinden
						SuchBaum rTB = new SuchBaum(root.getRchild());
						int minimal = rTB.getMinimum(); //Minimum des rechten Teilbaums
						rTB.delete(minimal); //minimalsten Wert aus rechten Teilbaum loeschen
						//minimalsten Wert als neue Wurzel setzen
						root.setKey(minimal);
					}
				} else { //wenn beide Teilbaeume null
					root = null;
				}		
			} else {
				if(key < root.getKey()) {
					SuchBaum lTB = new SuchBaum(root.getLchild());
					lTB.delete(key);
					root.setLchild(lTB.getRoot());
				} else {
					SuchBaum rTB = new SuchBaum(root.getRchild());
					rTB.delete(key);
					root.setRchild(rTB.getRoot());
				}
			}
		}
	}

	private int getMinimum() {
		Node minimal = root;
		while(minimal.getLchild() != null) {
			minimal = minimal.getLchild();
		}
		return minimal.getKey();
	}
}

```
