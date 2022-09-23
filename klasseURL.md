# Klasse URL und URLConnection

...repräsentiert "Uniform Resource Locator".


## URL

...Link zu Ressource im World Wide Web.

[https://][www.javatpoint.com/][java-tutorial]\
[Protocol][Host Name][File]

- Ressource z.B.:
  - Datei
  - Verzeichnis
  - Abfrage Datenbank
  - Suchmaschine

## URLConnection

...besitzt Methoden, die einen von der Ressource der URL lesen und auf diese schreiben lassen.\

bspw.: openConnection()

## Auf Daten einer URL mit Java zugreifen

- Kombi aus _InputStreamReader_ und _BufferedReader_.

1. URLConnectionReader Objekt erstellen
2. URL Objekt mit URL, auf welche man zugreifen will, erstellen
3. Benutze dieses URL Objekt, um URLConnection Objekt zu erstellen
4. Nutze InputStreamReader und BufferedReader, um von URL Verbindung zu lesen
5. readLine()-Methode des BufferedReader gibt String zurück, ist dieser gleich _null_ bedeutet das, dass man das Ende des Dokuments erreicht hat
6. Füge Strings, die man als Output von URL erhalten aht zu StringBuilder Objekt zusammen

**oder besser:**

1. URL-Objekt für Webdokument erstellen
2. openStream() Methode der URL-Klasse nutzen - ist InputStream
3. Diesen InputStream zum Weiterverarbeiten nutzen und Daten auslesen
4. Files.copy(InputStream in, Path target, CopyOption options) kopiert alle Bytes eines InputStreams in Datei

## Zusammenfassung

- URL-Klasse repräsentiert Link zu Ressource im World Wide Web, dem "Uniform Resource Locator"
- URLConnection-Klasse besitzt Methoden, die einen ermöglichen von der Ressource der URL zu lesen und auf diese zu schreiben.
- Auf Daten einer URL mit Java zugreifen
  - URL-Objekt für Webdokument
  - InputStream für Webdokument erstellen (openStream() von URL-Klasse)
  - InputStream zum Auslesen
  - Files.copy(InputStream in, Path target, CopyOption options) kopiert schlussendlich alle Bytes eines InputStreams in Datei
