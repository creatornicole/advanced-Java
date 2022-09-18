# Beispielumsetzung einer Nachbarschaftsliste in Java

...eine Nachbarschaftsliste dient der Darstellung eines Graphen, indem in dieser zu jedem Knoten des Graphen die verbundenen Knoten aufgelistet werden.

```java
/*
* bei Umsetzung ist Datei von folgender Form verwendet wurden:
* erste Zeile: Knotenanzahl des Graphen
* zweite Zeile: Kantenanzahl des Graphen
* jede weitere Zeile beinhaltet jeweils zwei Knoten, die miteinander verknuepft sind
*/

public class GraphListen {

	private int knotenanzahl;
	private int kantenanzahl;
	private ArrayList<HashSet<Integer>> nachbarknoten;
	
	public GraphListen(String file) throws NumberFormatException, IOException {
		//liest Datei ein
		Scanner sc = new Scanner(new File(file));
		//speichert Anzahl der Knoten und Kanten in Variablen
		this.knotenanzahl = sc.nextInt(); //Knoten sind erste Zahl auf ersten Zeile in Datei
		this.kantenanzahl = sc.nextInt(); //Kanten sind zweite Zeile auf zweiten Zeile in Datei

		nachbarknoten = new ArrayList<HashSet<Integer>>();
		HashSet<Integer> nachbarn;

		for(int i = 0; i < knotenanzahl; i++) {
			nachbarknoten.add(i, new HashSet<Integer>());
		}

		for(int i = 0; i < kantenanzahl; i++) {
			int knoten1 = sc.nextInt();
			int knoten2 = sc.nextInt();

			nachbarn = nachbarknoten.get(knoten1);
			nachbarn.add(knoten2);

			nachbarn = nachbarknoten.get(knoten2);
			nachbarn.add(knoten1);
		}
	}

	/**
	 * Gibt Anzahl der Knoten zurueck
	 *
	 * @return Knotenanzahl
	 */
	public int getKnotenanzahl() {
		return knotenanzahl;
	}

	/**
	 * Gibt Anzahl der Kanten zurueck
	 *
	 * @return Kantenanzahl
	 */
	public int getKantenanzahl() {
		return kantenanzahl;
	}

	/**
	 * Testet, ob die Knotennummer zwischen 0 und Anzahl der Knoten liegt
	 *
	 * @param knoten
	 * @return
	 */
	public boolean existsVertex(int knoten) {
		if((knoten >= 0) && (knoten < knotenanzahl))
			return true;
		else
			return false;
	}

	/**
	 * Fuegt Kante zwischen uebergebenen Knoten der Liste hinzu
	 *
	 * @param knoten1
	 * @param knoten2
	 */
	public void addEdge(int knoten1, int knoten2) {
		HashSet<Integer> nachbarn;
		//get nachbarliste knoten1
		nachbarn = nachbarknoten.get(knoten1);
		//fuege knoten2 zu nachbarliste knoten1 hinzu, wenn knoten2 auf dieser noch nicht existiert
		if(!(nachbarn.contains(knoten2)))
			nachbarn.add(knoten2);
		//get nachbarliste knoten2
		nachbarn = nachbarknoten.get(knoten2);
		//fuege knoten1 zu nachbarliste knoten1 hinzu, wenn knoten1 auf dieser noch nicht existiert
		if(!(nachbarn.contains(knoten1)))
			nachbarn.add(knoten1);
	}

	/**
	 * Gibt Nachbarschaften des uebergebenen Knoten zurueck
	 *
	 * @param knoten
	 * @return
	 */
	public String getNachbarschaften(int knoten) {
		HashSet<Integer> nachbarn = nachbarknoten.get(knoten);
		return nachbarn.toString();
	}

	/**
	 * Gibt Grad (Anzahl der angrenzenden Kanten) des Knotens zurueck
	 *
	 * @param knoten
	 * @return
	 */
	public int getGrad(int knoten) {
		HashSet<Integer> nachbarn = nachbarknoten.get(knoten);
		return nachbarn.size();
	}

	/**
	 * Gibt Graphen geeignet formatiert zurueck
	 *
	 * @return
	 */
	public String toString() {
		HashSet<Integer> nachbarn;
		StringBuilder graph = new StringBuilder();
		String strNachbarn;
		for(int i = 0; i < knotenanzahl; i++) {
			nachbarn = nachbarknoten.get(i);
			strNachbarn = nachbarn.toString();
			graph.append(i + " " + strNachbarn + "\n");
		}
		return graph.toString();
	}
}
```
