# XML

...ist eine extensible markup language und stellt eine externe Datenstruktur in Java dar.

- XML = extensible markup language
- stark vereinfachte markup language
- dient Speicherung, Übertragung, Rekonstruktion von beliebigen Daten

- lesbar von Mensch und Maschine

- Verwaltung durch W3C (World Wide Web Consortium)

## Anwendungsfelder

Bsp.:
- Websites
- Grafik
- Web Services
- Konfigurationen

## Syntax

<Start-Tag> Inhalt <End-Tag>

Bsp.:
```XML
<employees>
  <employee>
    <firstName>Michael</firstName> <lastName>Peters</lastName>
  </employee>
  <employee>
    <firstName>Peter</firstName> <lastName>Michels</lastName>
  </employee>
  <employee>
    <firstName>Michelle</firstName> <lastName>Peterson</lastName>
  </employee>
</employees>
```

## Elemente und Attribute

| Bezeichnung    | Beschreibung                                                                                           |
|----------------|--------------------------------------------------------------------------------------------------------|
| Element (Tag)  | kann beliebig (auch keine) Kind-Elemente und/oder Attribute haben                                      |
| Leeres Element | keine Attribute und Kindelemente                                                                       |
| Root Element   | nur einmal in XML Dokument enthalten, umfasst alle anderen Elemente                                    |
| Attribute      | können Elementen hinzugefügt werden, Attributnamen in Element müssen eindeutig sein (unterschiedlich)  |

## Spezifikation

- gibt Tag-Anordung vor
- Tags können i.d.R. frei bzw. auf das Fach bezogen benannt werden
- Semantik (Inhalt) sehr flexibel
- Syntax (Grammatik) sehr streng
- beachten von:
  - Grammatikgültigkeit (Wohlgeformtheit)
  - Inhaltsgültigkeit (Gültigkeit)


## Programmierschnittstellen

Bsp.:
| Bezeichnung | Erläuterung |
|-------------|-------------|
| DOM         | Document Object Model, "DOM defines a platform-neutral model for events, aborting activities, and node trees." (https://dom.spec.whatwg.org/) |
| SAX         | Simple API für XML, eventbasiert                                                                                                              |
| StAX        | Streaming API für XML, Zwischenweg DOM und SAX                                                                                                |
| XLST        | extensible Stylesheet Language Transformation, tranformiert JSON-Dokument in neues Dokument (bspw.: pdf, txt)                                 |
| XPath       | XML Path Language, ermöglicht durchlaufen Baum, um definierte Elemente/Attribute zu finden, ohne alle Elemente zu bearbeiten                  |

## Zusammenfassung

- XML = extensible markup language
- dient Speicherung, Übertragung, Rekonstruktion von beliebigen Daten
- leichter lesbar
- Anwendungsfelder u.a.: Websites, Grafik, Web Services, Konfigurationen
- XML-Dokument besteht aus Root-Element, welches alle anderen Elemente (Tags) mit eventuellen Attributen und Kindelementena, aber auch leere Elemente enthält.
- Tags meist frei wählbar
- Semantik = Inhalt sehr flexibel wählbar
- Syntax = Grammatik sehr streng
