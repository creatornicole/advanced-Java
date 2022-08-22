# Zeichenkettensuche

...umfasst die Suche in Texten.

- Begriff _Text_ = strukturierte Folgen beliebiger Länge von Zeichen aus einem endlichen Alphabet
- Alphabet = Buchstaben und/oder Zeichen und/oder zahlreiche Sonderzeichen
- zugrundliegenden Datentyp von Anwendungen, die mit Texten arbeiten, ist _String_ (Zeichenkette)
- Bereitstellung dieses Datentyps _String_ auf verschiedene Art und Weise möglich, als...
  - Grundtypen der Sprache
  - File-Of-Characters
  - Array-Of-Characters
  - verkettete Liste von Zeichen

## Suchproblem

- gegeben:
  - Zeichenkette a1...an von Zeichen aus endlichen Alphabet
  - Zeichenkette, das Muster (pattern) b1...bm mit jedes b Element Alphabet
- gesucht:
  - sind eine oder alle Vorkommen von b1...bm in a1...an, d.h. Indizes i mit 1 <= i <= (n-m+1) und ai=b1,ai+1=b2,...,ai+m-1=bm

## Suchen in dynamischen Texten

- Änderungen häufig und erheblich
- kann sich lohnen, Suchalgorithmen von Struktur des Musters und zugrundliegenden Alphabet abhängig zu machen

- Bsp.: durch Texteditoren manipulierter Text

| Algorithmus                  | Verfahren |
|------------------------------|-----------|
| Naive Suche                  |           |
| Knuth-Morris-Pratt Verfahren |           |
| Boyer-Moore Verfahren        |           |
| Bad Match Suche              |           |

## Suchen in statischen Texten

- Änderungen im Verhältnis zum Gesamtumfang geringfügig
- kann sein, dass es sich lohnt, den Text durch Hinzufügen von geeigneter Information (Index) so aufzubereiten, sodass die Suche verschiedener Muster gut unterstützt wird und nicht Durchsuchen des gesamten Textes erfordert

- Bsp.: Wörterbuch

## Zusammenfassung
