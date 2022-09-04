# Umwandlung txt-File in xml-File mit Java

## Beispiel

```java
/**
 * Liest Datei ein, welche zeilenweise Filme, mit Filmnamen, Jahr und SchauspielerInnen enthält.
 *
 * Aufbau eines Datensatzes in Datei:
 * [Name des Films] ([Jahr])/[Nachname Schauspieler 1],[Vorname Schauspieler 1]/[Nachname Schauspieler 2], [Vorname Schauspieler 2]/ ...
 *
 * @author ngott
 * @since 2022-09-02
 */

public class XMLUmwandlung {

	BufferedReader in;
	StreamResult out; //speichert Transformationsergebnis zwischen (kann XML, Text, HTMl oder andere Markup-Form sein)
	TransformerHandler th; //wartet auf SAXContentHandler Schreibevents und transformiert diese zu Ergebnis

	public void datenEinlesen(String file) {
		try {
			in = new BufferedReader(new FileReader(file));
			out = new StreamResult("D:\\___\\studium\\IF21wS1-B\\2_weiterfuehrendeProgrammierung\\NEU\\arbeitsordner\\filme.xml");

			oeffneXMl();

			String eintrag = in.readLine();
			String filmtitel;
			String jahr;
			ArrayList<String> schauspieler;
			StringTokenizer tokenizer;
			while(eintrag != null) {
				schauspieler = new ArrayList<String>();
				tokenizer = new StringTokenizer(eintrag, "()/");
				if(tokenizer.hasMoreTokens()) {
					filmtitel = tokenizer.nextToken();
					jahr = tokenizer.nextToken();
					while(tokenizer.hasMoreTokens()) {
						schauspieler.add(tokenizer.nextToken());
					}
					datenUebertragen(filmtitel, jahr, schauspieler);
				}
				eintrag = in.readLine();
			}
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				in.close();
			} catch (IOException e) {
				e.printStackTrace();
			} finally {
				schliesseXML();
			}
		}
	}

	public void oeffneXMl() {
		try {
			SAXTransformerFactory tf = (SAXTransformerFactory) SAXTransformerFactory.newInstance(); //fuer Transformation in XML
			th = tf.newTransformerHandler(); //zum Verarbeiten der SAXContentHandler Events zu Ergebnis

			Transformer transformer = th.getTransformer(); //Transformer zu Handler erhalten, um Parameter und Output Properties zu setzen
			transformer.setOutputProperty("{http://xml.apache.org/xslt}indent-amount", "4");
			transformer.setOutputProperty(OutputKeys.INDENT, "yes");

			th.setResult(out); //out - Ergebnis
			th.startDocument(); //XML-Datei starten
			th.startElement(null, null, "filme", null); //Root-Element filme setzen

		} catch (TransformerConfigurationException e) {
			e.printStackTrace();
		} catch (SAXException e) {
			e.printStackTrace();
		}
	}

	public void datenUebertragen(String titel, String jahr, ArrayList<String> schauspieler) {
		try {
			th.startElement(null, null, "film", null); //ATTRIBUTE NOCH HINZUFUEGEN

			th.startElement(null, null, "name", null);
			th.characters(titel.toCharArray(), 0, titel.length());
			th.endElement(null, null, "name");

			th.startElement(null, null, "aktuere", null);
			//solange Elemente in ArrayList vorhanden sind, Aktuer hinzufuegen
			for(int i = 0; i < schauspieler.size(); i++) {
				th.startElement(null, null, "aktuer", null);
				String aktuer = schauspieler.get(i);
				th.characters(aktuer.toCharArray(), 0, aktuer.length());
				th.endElement(null, null, "aktuer");
			}
			th.endElement(null, null, "aktuere");

			th.endElement(null, null, "film");

		} catch (SAXException e) {
			e.printStackTrace();
		}
	}

	public void schliesseXML() {
		try {
			th.endElement(null, null, "filme"); //End-Tag des Root-Elements filme hinzufuegen
			th.endDocument(); //XML-Datei schliessen

		} catch (SAXException e) {
			e.printStackTrace();
		}

	}
}
```

## Spezielle Klassen zur Problemlösung

- [StreamResult](https://docs.oracle.com/javase/7/docs/api/javax/xml/transform/stream/StreamResult.html)
- [TransformerHandler](https://docs.oracle.com/javase/7/docs/api/javax/xml/transform/sax/TransformerHandler.html)
- [ContentHandler](https://docs.oracle.com/javase/7/docs/api/org/xml/sax/ContentHandler.html)
- [SAXTransformerFactory](https://docs.oracle.com/javase/7/docs/api/javax/xml/transform/sax/SAXTransformerFactory.html)
- [TransformerFactory](https://docs.oracle.com/javase/7/docs/api/javax/xml/transform/TransformerFactory.html)

## Credit

- [Kurtiss Stackoverflow](https://stackoverflow.com/questions/23951132/a-simple-example-of-txt-to-xml-with-java)

## Zusammenfassung
