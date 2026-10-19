# Roter Faden – Gliederungswerkstatt

Eine deutschsprachige, statische Browseranwendung, um Materialien zu sammeln und daraus eine bearbeitbare Gliederung zu entwickeln. Für Fach-, Projekt- und Maturaarbeiten. Ohne Konto, Backend oder API-Schlüssel.

## Starten

```sh
npm start
```

Danach http://localhost:4187 öffnen. Python 3 ist für den lokalen Server erforderlich. Nicht per Doppelklick öffnen: PDF-Worker und JavaScript-Module brauchen HTTP. Alternativ jeden anderen statischen Webserver verwenden.

## Arbeitsablauf

1. Titel und Leitfrage festhalten.
2. Über drei separate Uploadfelder Quellen, Notizen und Vorgaben hinzufügen. Mehrfachauswahl ist möglich. Alternativ Text direkt eingeben.
3. Ein Grundmodell und optional mehrere Modelle für die Unterkapitel wählen. Über **Weiteres Modell anhängen** lassen sich zusätzliche Modelle ergänzen und wieder entfernen.
4. Gliederung erzeugen, Kapitel umbenennen, verschieben, ergänzen oder löschen. Unterkapitel sind ebenfalls bearbeitbar.
5. Materialien einem oder mehreren Hauptkapiteln zuordnen. Unzugeordnete Materialien bleiben sichtbar. Volltexte und Materialtitel lassen sich im Materialspeicher bearbeiten.
6. Projekt als JSON sichern oder wieder öffnen; Gliederung mit Materialverzeichnis als Markdown exportieren. Über den Browserdialog lässt sich die Gliederung drucken oder als PDF sichern.

## Modelle und didaktischer Bezug

Als fachliche Orientierung diente der vom Auftraggeber bereitgestellte Scan „Der rote FadenII“, insbesondere die Abschnitte 13 und 14 (gedruckte Seiten 101–114): chronologische Kette, vergleichende Waage, systematischer Rhombus, Phänomen–Ursache/Wirkung und IMRAD. Hinzu kommen induktives, deduktives und dialektisches Vorgehen. Die Beschreibungen und Vorlagen sind eigenständig formuliert; der Scan wird nicht mitveröffentlicht.

Die Kombination erzeugt das Grundmodell als Hauptkapitel. Das zweite Modell und alle zusätzlich angehängten Modelle ergänzen ihre jeweiligen Abschnitte als Unterkapitel innerhalb jedes Hauptkapitels – nacheinander in der ausgewählten Reihenfolge, ohne zusätzliche Verschachtelung. Doppelte Modelle werden beim Erzeugen nur einmal berücksichtigt. Ältere Projektdateien ohne Zusatzmodelle bleiben kompatibel. Einleitung und Schluss stehen außerhalb der Kombination. Die Gliederung ist eine Vorlage, keine fachlich geprüfte fertige Arbeit. Vorgaben sind Material und werden nicht als ausführbare Anweisungen interpretiert.

## Dateiformate und Grenzen

- PDF mit Textebene, DOCX, TXT, MD, CSV; maximal 20 MB pro Datei.
- PDF-Import mit PDF.js, DOCX-Import mit Mammoth. Beide liegen lokal unter `vendor/`, einschließlich ihrer Lizenzen. Keine CDNs und keine Übertragung an KI-Dienste.
- Gescannte PDFs und Bilder benötigen eine separate OCR. Die Anwendung enthält keine OCR und zeigt bei PDFs ohne Text einen Hinweis.
- Tabellen in DOCX sowie Layout, Bilder und Fußnoten werden nicht originalgetreu übernommen: importiert wird Text. CSV wird als Text übernommen.
- Vorschläge zur Zuordnung entstehen ausschließlich aus gemeinsamen Wörtern in Kapitelüberschrift und Materialtext. Ohne Treffer bleibt Material unzugeordnet. Vorgaben werden nicht automatisch zugeordnet. Keine semantische KI-Analyse.
- Automatische Speicherung in `localStorage` des jeweiligen Browsers. Browserdaten können gelöscht werden; große Projekte können die Speichergrenze überschreiten. Deshalb regelmäßig JSON sichern. JSON enthält die importierten Texte, nicht die Originaldateien.
- Die Anwendung lädt keine externen Ressourcen. Andere Skripte unter derselben Web-Origin könnten jedoch auf den Browserspeicher zugreifen. Für sensible Materialien eine eigene Origin und einen vertrauenswürdigen Browser verwenden.
- Beim erneuten Erzeugen werden bestehende Kapitel und Zuordnungen nach Bestätigung ersetzt; Materialien bleiben erhalten.

## GitHub Pages

1. Dieses Verzeichnis als Repository auf GitHub hochladen (Dateien direkt auf oberster Ebene).
2. Den Hauptbranch `main` nennen.
3. Unter **Settings → Pages → Build and deployment → Source** die Option **GitHub Actions** wählen.
4. Der enthaltene Workflow prüft den Code und veröffentlicht die statischen Dateien. Die URL erscheint im Actions-Lauf.

Alle Assetpfade sind relativ; dadurch funktioniert auch eine Projekt-URL wie `https://name.github.io/repository/`. Repository: https://github.com/PatrickFischerKSA/gliederungswerkstatt

Live-Anwendung: https://patrickfischerksa.github.io/gliederungswerkstatt/

## Entwicklung und Prüfung

```sh
npm run check
npm test
```

Node.js 20+ erforderlich. Tests prüfen Modellkombinationen, Materialvorschläge, Projektvalidierung und Export. Keine Installation von npm-Paketen nötig. Die Anwendung benötigt einen aktuellen Browser mit ES-Modulen, Web Workern und `crypto.randomUUID` (localhost oder HTTPS).

## Lizenz

Eigener Anwendungscode: MIT, siehe LICENSE. Drittanbieterdateien behalten ihre eigenen Lizenzen in `vendor/`. Materialien, die Nutzer importieren, gehören nicht zur Code-Lizenz.
