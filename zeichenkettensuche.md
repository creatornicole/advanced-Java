# Zeichenkettensuche

...umfasst die Suche in Texten.

- Texte lassen sich als Folge von Zeichenketten verstehen.
- Zeichenketten dabei als beliebige Aneinanderreihung beliebig vieler Zeichen aus endlichen Alphabet.

- Voraussetzung Zeichenkette bei Textsuche:
  - nicht negative, ganzzahlige Länge
  - Zugriff auf i-te Zeichen einer Zeichenkette für jedes i >= 1 möglich

## Begriffe

| Begriff | Erklärung |
|---------|---------------------------|
| Text              | Folge von Zeichenketten |
| Zeichenkette      | beliebige Aneinanderreihung beliebig vieler Zeichen aus einem endlichen Alphabet |
| String processing | Algorithmen zur Verarbeitung von Zeichenketten |

- verschiedene Algorithmenarten zur Zeichenkettenverarbeitung:
  - Suche in Texten bzw. Erkennen bestimmter Muster (pattern matching)
  - Verschlüsseln, komprimieren von Texten
  - Analyse von Texten
  - Übersetzen von Texten

## Suchproblem

...kann bei der Suche in Texten wie folgt formuliert werden:

- Gegeben:
  - Text als Zeichenkette a1...aN
  - Zeichenkette bestehend aus Zeichen aus endlichen Alphabet
  - Muster als Zeichenkette b1...bM (mit bi Element des endlichen Alphabets und 1<= i <= M)

- Gesucht:
  - ein oder alle Vorkommen von b1...bM in a1...aN
  - d.h. Indizes i mit 1 <= i <= (N - M + 1)
  - und ai = b1 mit ai+1 = b2, ... , ai+M-1 = bM

- i.d.R. Länge N des Textes viel größer als Länge M des Musters

## Textarten

- statischer Text
  - Änderungen verhältnismäßig selten
  - Änderungen im Verhältnis zum Gesamtumfang geringfügig
  - Bsp.: Wörterbuch
- dynamischer Text
  - Änderungen verhältnismäßig häufig
  - Änderungen im Verhältnis zum Gesamtumfang erheblich
  - Bsp.: Texteditoren

## Suche in dynamischen Text

- bei der Suche in dynamischen Texten kann es sich lohnen, Suchalgorithmen von zwei Dingen abhängig zu machen:
  - Struktur des Musters
  - zu Grunde liegende Alphabet

- Suchalgorithmen zur Suche in dynamischen Text:
  - Naive Verfahren
  - Knuth-Morris-Pratt (KMP)
  - Boyer-Moore

### Naive Verfahren zur Textsuche

...sucht Muster in Text, indem man das Muster, beginnend beim ersten Zeichen des Textes, der Reihe nach an jeden Teilstring des Texte (mit Länge M) legt und zeichenweise von links nach rechts vergleicht.
Entweder findet man so eine Übereinstimmung oder es kommt zu einem sogenannten Mismatch.

- sucht Muster solange in Text, bis Vorkommen des Musters in Text gefunden wurde oder das Ende des Textes erreicht wurde
- Muster (N - M + 1)-mal an Text anlegen und jeweils ganz durchlaufen
  - daraus ergibt sich Anzahl der Vergleiche
  - Anzahl der Vergleiche: (N - M + 1) * M
- Laufzeit: O(N * M)
- naive Verfahren ist gedächtnislos
  - d.h. selbe Textstelle wird unter Umständen mehrfach inspiziert
  - d.h. Verfahren merkt sich nicht, welche Zeichen im Text bereits mit Anfangsstück des Musters übereinstimmte bis Mismatch auftrat

- Verbesserungsmöglichkeit: Muster bei Vergleich nicht komplett, sondern nur bis zu ersten Mismatch durchlaufen
  - Anzahl der Vergleiche verändert sich zu: O(M + N)






## Zusammenfassung

- Suchproblem
  - gegeben: Text, endliches Alphabet, Muster
  - gesucht: Muster im Text
- i.d.R. Text viel länger als Muster
- zwei Textarten
  - statisch -> Änderungen verhältnismäßig selten und geringfügig
  - dynamisch -> Änderungen verhältnismäßig häufig und erheblich






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
