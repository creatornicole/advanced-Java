# Aufwand von Algorithmen

...wird beachtet, wenn für eine Aufgabenklasse der beste existierende Algorithmus herausgefunden werden soll.

- Bedarf an Speicher und Rechenzeit eines Algorithmus abhängig von...
  - Implementierung in Programmiersprache
  - Rechner, der das Programm ausführt

- genaue quantitative Aussagen schwierig
  - deswegen keine realen Laufzeiten und Speichervolumen
  - sondern Größenordnungen in Abhängigkeit von Umfang und Art der Eingabedaten
  - Idealisierung des Ccomputers als "abstrakte Maschine", bei der alle Operationen die gleiche Zeiteinheit und alle elementaren Daten den gleichen Speicherplatz brauchen.

- Aufpassen: Was mit kleinen Eingabemengen noch gut funktioniert, kann bei Anwachsen der Eingabemenge rasch zu einem Problem werden

## Begriffe

| Begriff                           | Erklärung                                                                                            |
|-----------------------------------|------------------------------------------------------------------------------------------------------|
| Dimension (Umfang) eines Problems | Anzahl oder Größe n der Eingabedaten                                                                 |
| Aufwand eines Algorithmus         | Anzahl T(n) von Zeit- bzw. Speichereinheiten bei seiner Durchführung für ein Problem der Dimension n |
| Komplexität einer Problemklasse   | Kleinstmöglicher Aufwand von Algorithmen, die jedes konkrete Problem dieser Klassen lösen können     |

- in T(n) wird im Allgemeinen nur der am stärksten wachsende Teil betrachtet
  - asymptotischer Aufwand des Algorithmus interessant
  - also Verhalten n -> unendlich

## Mögliche Kriterien

- Speicheraufwand
  - Speicherbedarf für Programm (konstant)
  - Speicherbedarf für Dateien
    - abhängig von Eingabewerten -> Speicherkomplexität
- Zeitaufwand
  - abhängig von Eingabewerten -> Rechenkomplexität

## O-Notation

...soll dem Ziel dienen eine möglichst einfache Klassifizierung des Aufwandes für unterschiedliche Algorithmen zu finden.

- Summenregel
  - O(f(n)) + O(h(n)) = O(f(n) + h(n))
  - jeweils nur der höchste konstante Faktor spielt eine Rolle für Komplexität des Algorithmus

- Produkregel
  - k * O(f(n)) = O(f(n))
  - O(f(n)) * O(h(n)) = O(f(n) * h(n))
  - konstante Faktoren spielen keine Rolle für die Komplexität des Algorithmus

## Aufwandsklassen

| O-Notation   | Aufwand          |
|--------------|------------------|
| O(1)         | konstant         |
| O(log2(n))   | logarithmisch    |
| O(n)         | linear           |
| O(n*log2(n)) | n-log(n)         |
| O(n^2)       | quadratisch      |
| O(n^3)       | kubisch          |
| O(e^n)       | exponentiell     |

## Zusammenfassung

- Aufwand von Algorithmen betrachten, um den Besten für zu lösende Problem zu finden
- Dabei Idealisierung des Computers als "abstrakte Maschine", bei der alle Operationen die gleiche Zeiteinheit und alle elementaren Daten den gleichen Speicherplatz brauchen
  - Speicheraufwand (konstanten und für Dateien)
  - Zeitaufwand
- O-Notation für möglichst einfach Klassifizierung des Aufwandes unterschiedlicher Algorithmen genutzt
