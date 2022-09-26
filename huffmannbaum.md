# Huffmann Baum

...stehen die Blätter für die zu kodierenden Zeichen, während der Pfad von der Wurzel zum Blatt das Codesymbol bestimmt.

## Huffmann Codierung

1. Zählen der einzelnen Zeichen
2. Tipp: Zum besseren Aufbau des Baumes die Zeichen nach der Anzahl sortieren
3. Die beiden kleinsten Elemente auswählen und neuen Knoten bilden
4. Solange Schritt 3, bis Baum erstellt
5. Alle linken Verzweigungen bekommen den Wert 0, alle rechten Verzweigungen den Wert 1
6. Alle Zeichen der Zeichenkette im Baum suchen, Weg dahin (also Folge von 0 und 1) ausgehend von Wurzel kodiert Zeichen

## Zusammenfassung

- Huffmann Baum entsteht aus und dient dem Prozess der Huffmann Codierung
- Huffmann Codierung codiert Zeichenkette zu Folge aus 0 und 1
