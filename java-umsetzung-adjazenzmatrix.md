# Beispielumsetzung für Adjazenzmatrix in Java

...unter einer Adjazenzmatrix versteht man eine Darstellungsform eines Graphen, welche die verbundenen Knoten in Form einer 2-dimensionalen Matrix darstellt.

```java
public class Graph {

	private int knotenanzahl; //Anzahl der Knoten
	private boolean[][] adjazenzmatrix; //Adjazenzmatrix des Graphen = moegliche Darstellungsform

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Graph g = new Graph(3);
		g.dreierKreisErzeugen();
		g.anzeigeMatrix();
	}

	/**
	 * Konstruktor erzeugt fuer Graphen mit k Knoten eine leere Adjazenzmatrix
	 *
	 * @param knoten Knotenanzahl des Graphen
	 */
	public Graph(int knoten) {
		this.knotenanzahl = knoten;
		this.adjazenzmatrix = new boolean[knotenanzahl][knotenanzahl];
	}

	/**
	 * Methode zum Einfuegen einer Kante zwischen Knoten knoten1 und Knoten knoten2
	 *
	 * @param knoten1 einer der zwei Knoten, zwischen denen Kante eingefuegt werden soll
	 * @param knoten2 einer der zwei Knoten, zwischen denen Kante eingefuegt werden soll
	 * @return Wahrheitswert, ob Einfuegen der Kante erfolgreich war
	 */
	public boolean einfuegenKante(int knoten1, int knoten2) {
		if(knotenVorhanden(knoten1, knoten2)) {
			if(kanteVorhanden(knoten1, knoten2)) { //entsprechend Nachricht ausgeben, wenn Kante bereits vorhanden ist
				System.out.println("Kante zwischen " + knoten1 + " und " + knoten2 + " bereits vorhanden.");
				return false;
			} else {
				//Kante ei1nfuegen heisst, Wert an Stelle in Adjazenzmatrix auf true setzen
				adjazenzmatrix[knoten1-1][knoten2-1] = true;
				//Achtung: Kante zwischen zwei Knoten ist in Adjazenzmatrix zweimal vermerkt
				adjazenzmatrix[knoten2-1][knoten1-1] = true;
				return true;
			}
		} else {
			System.out.println("Ein übergebener Knoten ist im Graphen nicht vorhanden.");
			return false;
		}		
	}

	/**
	 * Methoden zum Loeschen einer Kante zwischen Knoten knoten1 und Knoten knoten2
	 *
	 * @param knoten1 einer der zwei Knoten, zwischen denen Kante geloescht werden soll
	 * @param knoten2 einer der zwei Knoten, zwischen denen Kante geloescht werden soll
	 * @return Wahrheitswert, ob Loeschen der Kante erfolgreich war
	 */
	public boolean loescheKante(int knoten1, int knoten2) {
		if(!(kanteVorhanden(knoten1, knoten2))) { //entsprechend Nachricht ausgeben, wenn von Vornherein keine Kante vorhanden ist
			System.out.println("Kante zwischen " + knoten1 + " und " + knoten2 + " nicht vorhanden.");
			return false;
		} else {
			//Kante loeschen heisst, Wert an Stelle in Adjazenzmatrix auf false setzen
			adjazenzmatrix[knoten1-1][knoten2-1] = false;
			//Achtung: Kante zwischen zwei Knoten ist in Adjazenzmatrix zweimal vermerkt
			adjazenzmatrix[knoten2-1][knoten1-1] = false;
			return true;
		}
	}

	/**
	 * Gibt Wahrheitswert zurueck, ob Kante zwischen uebergebenen Knoten vorhanden ist oder nicht
	 *
	 * @param knoten1 einer der zwei Knoten, zwischen den kontrolliert werden soll, ob Kante vorhanden
	 * @param knoten2 einer der zwei Knoten, zwischen den kontrolliert werden soll, ob Kante vorhanden
	 * @return Wahrheitswert, ob Kante vorhanden ist oder nicht (true -> vorhanden, false -> nicht vorhanden)
	 */
	private boolean kanteVorhanden(int knoten1, int knoten2) {
		boolean kantenverweis1 = adjazenzmatrix[knoten1-1][knoten2-1]; //-1, da Index Matrix mit 0 startet, Knoten jedoch bei 1
		boolean kantenverweis2 = adjazenzmatrix[knoten2-1][knoten1-1];
		if(kantenverweis1 || kantenverweis2) {
			return true; //Kante vorhanden
		} else {
			return false; //Kante nicht vorhanden
		}
	}

	/**
	 * Gibt Wahrheitswert zurueck, ob Knoten in Graphen vorhanden sind
	 *
	 * @param knoten1
	 * @param knoten2
	 * @return Wahrheitswert, ob beide Knoten im Graphen vorhanden sind
	 */
	private boolean knotenVorhanden(int knoten1, int knoten2) {
		return ((knoten1 > knotenanzahl) || (knoten2 > knotenanzahl)
				|| (knoten1 < 1) || (knoten2 < 1))
				? false : true;
	}

	/**
	 * Gibt Adjazenzmatrix des Graphen auf Konsole aus
	 */
	public void anzeigeMatrix() {
		StringBuilder matrix = new StringBuilder();
		String zeile = "  ";

		//oberste Zeile mit Referenz auf Knoten erzeugen
		for(int i = 1; i <= knotenanzahl; i++) {
			zeile += " " + i;
		}
		matrix.append(zeile + "\n"); //Zeile zu Ausgabe der Matrix hinzufuegen

		//Zeilenweise Matrix durchlaufen
		for(int i = 0; i < knotenanzahl; i++) {
			zeile = ausgabeZeile(i);
			matrix.append(i+1 + "|" + zeile + "\n");
		}
		System.out.println(matrix);
	}

	/**
	 * Gibt Zeile mit entsprechender Zeilennummer der Adjazenzmatrix aus
	 *
	 * @param zeilennummer Zeile, die aus Adjazenzmatrix ausgegeben werden soll (Achtung: startend bei 0)
	 * @return Zeile der Adjazenzmatrix in Form 0/1
	 */
	private String ausgabeZeile(int zeilennummer) {
		String zeile = "";
		//Zeile durchlaufen und zu String zusammenbauen
		//Durchlaufen erfolgt spaltenweise
		for(int i = 0; i < knotenanzahl; i++) {
			zeile += (adjazenzmatrix[zeilennummer][i]) ? " 1" : " 0";
		}
		return zeile;
	}

	/**
	 * Erzeugt einfachen Graphen in folgender Form:
	 * - drei Knoten
	 * - jeder Knoten mit jeweils anderen beiden Knoten verbunden
	 * - ungerichteter, ungewichteter Graph
	 */
	public void dreierKreisErzeugen() {
		//alle Knoten mit allen anderen verbinden
		for(int i = 0; i < knotenanzahl; i++) { //alle Knoten des Graphen durchgehen
			for(int j = i+1; j < knotenanzahl; j++) { //alle Verknuepfungen zu allen anderen existierenden Knoten erstellen
				adjazenzmatrix[i][j] = true;
				adjazenzmatrix[j][i] = true;
			}
		}
	}

}
```
