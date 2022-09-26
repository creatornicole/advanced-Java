# Hashing

## Hashfunktion

...wird bspw. von HashSet genutzt, um Werte in Array einzuordnen.

Bsp.:\
gegeben:
- Hashfunktion h... h(x) = (x % 3) + (x % 4)
- Werte A = { 1, 2, 3, 4, 5, 6, 7 }

| Index | Wert |
|-------|------|
| 0     |      |
| 1     | 4    |
| 2     | 1, 6 |
| 3     | 3, 5 |
| 4     | 2, 7 |
| 5     |      |
| 6     |      |
| 7     |      |

Beobachtung:
- Kollisionen treten auf, d.h. Plätze in Array mehrmals belegt
Lösung:
- bessere Hashfunktion

## Zusammenfassung
