# Beispielumsetzungen elementarer-, effizienter- und spezieller Sortieralgorithmen fuer Zahlenarrays in Java

## Hilfsmethoden für Beispiele

```java
/**
	 * Vertauscht Werte des Arrays an Positionen i und j miteinander.
	 *
	 * @param zahlen Array der Elemente
	 * @param i Position des zu vertauschenden Elements
	 * @param j Position des damit zu vertauschenden Elements
	 */
	private static void vertauschen(int[] zahlen, int i, int j) {
		int hilf = zahlen[i];
		zahlen[i] = zahlen[j];
		zahlen[j] = hilf;
	}

	private static void vertauschen(Integer[] zahlen, int i, int j) {
		int hilf = zahlen[i];
		zahlen[i] = zahlen[j];
		zahlen[j] = hilf;
	}
```

## Elementare (einfache) Sortieralgorithmen
### Bubble-Sort

- mit Beenden des Durchlaufs, wenn keine Vertauschungen gemacht wurden

```java
/**
	 * Implementation des Bubble-Sort-Algorithmus mit Abbrechen des Verfahrens,
	 * wenn waehrend eines Durchlaufs keine Vertauschungen gemacht werden.
	 *
	 * @param zahlen Zu sortierendes Array ganzer Zahlen
	 */
	public static void bubbleSortMod(int[] zahlen) {
		int vertauschungen = 0; //Zaehlvariable, um Anzahl der Vertauschungen zu bestimmen
		int lokalVer = 0; //Vertauschungen waehrend eines Durchlaufs
		for(int i = zahlen.length-2; i >= 0; i--) { //Positionen in Array durchlaufen
			for(int j = 0; j <= i; j++) { //Element an Position mit restlichen Elementen in Abschnitt vergleichen und eventuell vertauschen
				if(zahlen[j] > zahlen[j+1]) {
					vertauschen(zahlen, j, j+1);
					System.out.println(Arrays.toString(zahlen)); //Array nach jeder Vertauschung ausgeben
					vertauschungen++;
					lokalVer++;
				}
			}
			if(lokalVer == 0)
				break;
			lokalVer = 0;			
		}
		System.out.println("Anzahl Vertauschungen = " + vertauschungen);

	}
```

### Selection-Sort

```java
/**
	 * Implementation des Selection-Sort-Verfahrens
	 *
	 * @param zahlen zu sortierendes Array
	 */
	public static void selectionSort(int[] zahlen) {
		for(int i = 0; i < zahlen.length; i++) {
			int minPos = minPositionAb(zahlen, i);
			if(minPos != i) {
				vertauschen(zahlen, i, minPos);
			}
		}
	}

	/**
	 * Hilfsmethode, um Position des kleinsten Elements ab einer bestimmten Position zu bestimmen
	 *
	 * @param zahlen zu sortierendes Array
	 * @param pos Position ab der Minimumwert gesucht werden soll
	 * @return Minimum
	 */
	private static int minPositionAb(int[] zahlen, int pos) {
		int minPos = pos;
		for(int i = pos + 1; i < zahlen.length; i++) {
			if(zahlen[i] < zahlen[minPos]) {
				minPos = i;
			}
		}
		return minPos;
	}
```

### Insertion-Sort

```java
/**
	 * Implementation des Insertion-Sort-Algorithmus
	 *
	 * @param zahlen Zu sortierende Array
	 */
	public static void insertionSort(int[] zahlen) {
		for(int i = 1; i <= zahlen.length-1; i++) {
			int j = i;
			int hilf = zahlen[i];
			while((j>0) && (zahlen[j-1]>hilf)) {
				zahlen[j] = zahlen[j-1];
				j = j-1;
				System.out.println(Arrays.toString(zahlen));
			}
			zahlen[j] = hilf;
		}
	}
```

## Effiziente Sortieralgorithmen
### Merge-Sort

```java
/**
 * Implementation des Merge-Sort-Verfahrens nach J. v. Neumann
 *
 * @param objekte zu sortierendes Array
 * @param links linke Abschnittsgrenze
 * @param rechts rechte Abschnittsgrenze
 */
public static void mergeSort(Integer[] objekte, int links, int rechts) {
  if(links < rechts) {
    int mitte = (links + rechts) / 2;
    mergeSort(objekte, links, mitte); //Aufrufen fuer jeweils "linke" Teilarray
    mergeSort(objekte, mitte + 1, rechts); //Aufrufen fuer jeweils "rechte" Teilarray

    merge(objekte, links, mitte, rechts); //Teilarrays zu Gesamtarray mischen
  }
}

/**
	 * Hilfsmethode fuer Merge-Sort-Verfahren.
	 * Mischt sortierte Array Abschnitte
	 *
	 * @param objekte
	 * @param links
	 * @param mitte
	 * @param rechts
	 */
	private static void merge(Integer[] objekte, int links, int mitte, int rechts) {
		Integer[] hilfsArray = new Integer[rechts-links+1];
		int linksindex = links;
		int rechtsindex = mitte + 1;
		int i = 0;
		//Mischen Teilarrays zu Gesamtarray
		while((linksindex <= mitte) && (rechtsindex <= rechts)) {
			if(objekte[linksindex] < objekte[rechtsindex]) {
				hilfsArray[i] = objekte[linksindex];
				linksindex++;
			} else {
				hilfsArray[i] = objekte[rechtsindex];
				rechtsindex++;
			}
			i++;
		}
		if(linksindex > mitte) {
			for(int j = 0; j <= (rechts-rechtsindex); j++) {
				hilfsArray[i+j] = objekte[rechtsindex+j];
			}
		} else {
			for(int j = 0; j <= (mitte-linksindex); j++) {
				hilfsArray[i+j] = objekte[linksindex+j];
			}
		}
		//Ueberschreiben Hilfsarray in richtiges Gesamtarray
		for(int j = 0; j <= (rechts-links); j++) {
			objekte[links+j] = hilfsArray[j];
		}
	}
```

### Quick-Sort

```java
/**
	 * Implementation des Quick-Sort-Verfahrens nach C.A.R. Hoare
	 * Pivot-Element dabei mittleres Element des uebergebenen Arrays
	 *
	 * @param zahlen zu sortierendes Array
	 * @param links linke Grenze des zu sortierenden Array-Abschnitts
	 * @param rechts rechte Grenze des zu sortierenden Array-Abschnitts
	 */
	public static void quickSortPivotMiddle(Integer[] zahlen, int links, int rechts) {
		if(links < rechts) {
			int linksindex = links;
			int rechtsindex = rechts;
			int pivot = zahlen[(links+rechts)/2]; //Pivot-Element ist mittleres Element des uebergebenen Arrays
			//In Grosse und Kleine teilen
			do {
				while(zahlen[linksindex] < pivot) { //von links ausgehend: erste Element >= Pivot-Element finden
					linksindex++;
				}
				while(zahlen[rechtsindex] > pivot) { //von rechts ausgehend: erste Element <= Pivot-Element finden
					rechtsindex--;
				}
				if(linksindex <= rechtsindex) {
					vertauschen(zahlen, linksindex, rechtsindex); //vertauschen der beiden ermittelten Elemente
					linksindex++;
					rechtsindex--;
				}
			} while(linksindex <= rechtsindex);
			//Rekursives Aufrufen zum Zweck der Sortierung
			quickSortPivotMiddle(zahlen, links, rechtsindex); //jeweils linke Teilarray sortieren
			quickSortPivotMiddle(zahlen, linksindex, rechts); //jeweils rechte Teilarray sortieren
		}
	}
```

## Spezielle Sortieralgorithmen
### Count-Sort

```java
/**
	 * Implementation Count-Sort-Verfahren.
	 * Geeignet fuer: nichtnegative ganze Zahlen
	 *
	 * @param zahlen zu sortierende Array
	 * @param max hoechste Zahl in zu sortierendem Array = Groesse Hilfsarray
	 */
	public static void countSort(int[] zahlen, int max) {
		int[] zaehler = new int[max+1];
		for(int i = 0; i <= max; i++)
			zaehler[i] = 0; //Zaehler fuer alle Zahlen auf 0 setzen
		for(int i = 0; i < zahlen.length; i++)
			zaehler[zahlen[i]] = zaehler[zahlen[i]] + 1; //zaehlen Anzahl Zahlen in Array
		int index = 0;
		for(int i = 0; i <= max; i++) { //zurueckschreiben Zahlen in Array
			for(int j = 0; j <= zaehler[i]-1; j++) {
				zahlen[index] = i;
				index++;
			}
		}
	}

	/**
	 * Maximalen Wert eines Zahlen-Arrays bestimmen
	 *
	 * @param zahlen zu sortierende Array
	 * @return Maximalwert des Zahlen-Arrays
	 */
	private static int max(int[] zahlen) {
		int maxBisher = zahlen[0];
		for(int zahl: zahlen) {
			if(zahl > maxBisher)
				maxBisher = zahl;
		}
		return maxBisher;
	}
```
