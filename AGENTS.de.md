[English](AGENTS.md) · [Español](AGENTS.es.md) · [Português](AGENTS.pt.md) · [Français](AGENTS.fr.md) · **Deutsch**

# AGENTS.md

Anleitung für KI-Agenten und Mitwirkende, die dieses Repository ändern.

## Was es ist

Eine statische Einzelseiten-Website zum Testen und Diagnostizieren von Bildschirmen (Smartphone, Computer und Fernseher). Alles liegt in `index.html`: HTML, CSS und JavaScript ohne Abhängigkeiten, ohne Bundler und ohne Netzwerkzugriffe.

## Struktur

- `index.html`: die gesamte Website.
- `README.md` (sowie `README.es.md`, `README.pt.md`, `README.fr.md`, `README.de.md`): Beschreibung und Funktionen für Nutzer.
- `AGENTS.md` (sowie `AGENTS.es.md`, `AGENTS.pt.md`, `AGENTS.fr.md`, `AGENTS.de.md`): Anleitung für Mitwirkende. Halte alle Sprachversionen synchron, wenn du eine änderst.
- `LICENSE`: GPL v3.

Innerhalb von `index.html` besteht das Skript aus diesen Teilen: Hilfsfunktionen, Sprachkern (`DICT`, `tr`, `applyLang`), Tests (`TOOLS`), Raster und Filter, Vollbild-Ansicht, Tastatur und Eingaben, Startseite, Menüs für Design und Sprache, Favicon und Start.

## Ausführen und testen

Es gibt keinen Build-Schritt. Öffne `index.html` im Browser oder stelle den Ordner mit `python3 -m http.server` bereit.

Prüfe vor dem Veröffentlichen von Änderungen mindestens Folgendes:

- Keine Fehler in der Konsole.
- Smartphone (~390 px), Computer (~1280 px) und Fernseher (~1920 px) ohne horizontales Scrollen.
- Helles, dunkles, reines Schwarz und automatisches Design. Bei ausgeschalteter Automatik bleibt das feste Design erhalten.
- Ein Browser ohne `matchMedia` fällt auf das helle Design zurück.
- Jeder Test öffnet sich im Vollbild, seine Bedienelemente reagieren und `Esc` schließt ihn.
- Geometrie und Kalibrierung: Das Feld ist auf Smartphone, Computer und Fernseher innerhalb des Kreises zentriert und zeigt Auflösung, Pixeldichte und Maßstab (mit `H` wird das Panel ausgeblendet, damit man es lesen kann).
- Sprachen: Ist das System in einer nicht unterstützten Sprache, verwendet die Website Englisch; das Menü listet zuerst Englisch, dann die Systemsprache und danach die übrigen auf; die Auswahl bleibt nach dem Neuladen erhalten.
- Eingaben funktionieren und die Hinweise wechseln: Tastatur, Touch (Wischen), TV-Fernbedienung (`ChannelUp`, `Info`, `GoBack` sowie Ereignisse nur mit Code 37–40/13 bei einem TV-User-Agent), Gamepad (simulierbar, indem `navigator.getGamepads` ersetzt wird).
- Wischraster: Ziehen malt Felder aus und wechselt weder den Test noch schließt es die Ansicht.

Playwright mit Chromium eignet sich, um diese Prüfungen zu automatisieren.

## Konventionen

- Eine einzige Datei, ohne externe Abhängigkeiten und ohne Netzwerkanfragen. Sie muss sich per Doppelklick öffnen lassen.
- Oberflächentext läuft über `tr(text)`. Der Schlüssel ist der spanische Text, klein geschrieben außer bei Eigennamen und Abkürzungen, und ohne Ausrufezeichen. Übersetzungen stehen in `DICT` (eine Tabelle pro Sprache). Fehlt eine Übersetzung, wird Spanisch angezeigt. Um eine Sprache hinzuzufügen: Ergänze `SUP`, `NATIVE` und `DICT` mit allen Schlüsseln und füge ein README und ein AGENTS in dieser Sprache hinzu.
- Farben und Design über CSS-Variablen in `:root`. Im Oberflächen-Code niemals feste Farben verwenden; Testmuster nutzen exakte Farben, weil sie das Produkt selbst sind.
- Designs: hell, dunkel (grau), reines Schwarz (`data-theme="black"`, Hintergrund #000) und automatisch. Die Automatik nutzt bei dunklem System das graue dunkle Design; das Kästchen **Reines Schwarz im dunklen Modus verwenden** im Designmenü ersetzt Dunkel durch reines Schwarz (`dt-oled` in `localStorage`). Es gibt keine Web-API zur OLED-Erkennung, daher entscheidet der Nutzer.
- Das Standarddesign ist hell. Die Automatik hängt von `prefers-color-scheme` ab; `data-theme="light|dark|black"` steht nur auf `<html>`, wenn der Nutzer das Design festlegt.
- Statische Muster werden als SVG mit `viewBox` gezeichnet und erhalten Breite und Höhe (`W`, `H`), damit sie zum tatsächlichen Seitenverhältnis des Bildschirms passen. Die Miniatur verwendet 160×90.
- Animierte Muster (`kind:"cv"`) werden auf einem `canvas` mit `init` und `frame` gezeichnet; ihre Miniatur ist ein statisches SVG (`thumb`).
- Barrierefreiheit: echte Schaltflächen, `aria-pressed` bei Auswahlelementen, sichtbarer Fokus, `aria-label` bei Miniaturen und Respekt vor `prefers-reduced-motion`.
- Speicherung mit `localStorage` immer innerhalb von `try/catch`; die Website muss auch ohne sie funktionieren. Gespeichert werden Design (`dt-theme`) und Sprache (`dt-lang`, `auto` oder ein Code).
- Sprache: Die Automatik folgt `navigator.languages`, mit Englisch als Rückfall. Statische Elemente verwenden `data-i18n`, `data-i18n-aria` und `data-i18n-title`. Bei einem Sprachwechsel wird `applyLang()` aufgerufen.
- Symbole sind Inline-SVGs mit `currentColor`. Verwende keine Symbolschriftarten und keine externen Bilder: Die Website besteht aus einer Datei und muss per Doppelklick identisch aussehen.
- Das Design wird über ein Aufklappmenü mit einem Symbol gewählt (`#themeBtn`, `#themeMenu`) mit `role="menu"`, Tastaturbedienung (Pfeiltasten, Esc), und das Symbol zeigt den aktuellen Modus. Das Sprachmenü (`#langBtn`, `#langMenu`) funktioniert genauso.
- Die Fußzeile wurde absichtlich entfernt. Bitte nicht wieder einfügen.
- Touch-Tests: Der Berührungszähler erzeugt einen Kreis pro Berührungspunkt und löscht die alten, wenn der Bildschirm erneut berührt wird; das Wischraster malt die Felder aus, die Finger oder Maus überqueren. Im Raster sind Wischgesten (navigieren, schließen) und Antippen zum Ein- und Ausblenden des Panels absichtlich deaktiviert.
- Spitzenhelligkeit: Der HDR-Modus verwendet `color(rec2100-pq 1 1 1)` nur, wenn `CSS.supports` das akzeptiert; andernfalls erscheint ein Hinweis und SDR-Weiß. Das Feld `help` eines Tests (hier `HDR_HELP`) wird in einem einklappbaren Bereich der Ansicht (`#vhelp`) angezeigt.
- `colorScale(x,y,w,h,noGray)` zeichnet die Farbreihen; mit `noGray` wird das Graustufenband weggelassen. Der RGB- und CMYK-Test hat eine Auswahl `Skala`, die über `ramp1` nur eine einzelne Skala anzeigt.
- Abspielen/Pausieren: Die Schaltfläche liegt in der Zeile `#vnav` zwischen Zurück und Weiter (Klasse `playbtn`), nicht im Bedienfeld. `clickPlay()` sucht sie dort.
- Die Kopfzeile hat keine Navigation nach Kategorien; Filter gibt es nur in der Seitenleiste und unter dem Raster. Bitte nicht wieder hinzufügen.
- Gemeinsame Hilfsfunktionen für Muster: `smpteSvg`, `grayStrip`, `colorScale`, `contrastSvg`, `geoBase`, `screenInfo`, `starCount` und `newStar`. Verwende sie wieder, statt Zeichencode zu duplizieren.
- Alle Eingaben (Tastatur, Maus, Touch, Fernbedienung, Gamepad und Joystick) laufen über den Verteiler `act(aktion, nativ)` mit den Aktionen `left`, `right`, `up`, `down`, `confirm`, `back`, `next`, `prev`, `toggle` und `playpause`. Um ein neues Gerät zu unterstützen, ordne es diesen Aktionen zu; keine losen Handler hinzufügen.
- `INPUT` speichert die zuletzt erkannte Eingabe (`keyboard`, `mouse`, `touch`, `remote`, `gamepad`) und wird in `data-input` auf `<html>` gespiegelt. Die Hinweise der Ansicht (`hintHtml`) hängen davon ab. Wenn du eine Aktion hinzufügst, ergänze ihren Hinweis für alle Eingaben.
- Tasten der Fernbedienung: `keyAction` akzeptiert den Namen (`ArrowLeft` oder `Left`) und den numerischen Code (37–40, 13). Manche Fernseher senden nur den Code; entferne diesen Ersatzmechanismus nicht.
- Warnung zur Photosensitivität: Der allgemeine Hinweis steht über dem Raster. Bewegungs- oder Farbwechsel-Tests haben ein `warn` und zeigen es in der Ansicht (`#vwarn`) mit derselben Klasse `.warn` wie die Startseite.
- Schaltflächen der Ansicht (`#vc .btn`), Pausenknopf und ausgewählte Schaltflächen: Blau der Regler `#85b7eb` mit schwarzem Text (sonst weiß mit schwarzem Text). Tastenhinweise (`kbd`) sind weiß mit schwarzem Text und flach, ohne unteren Rand.
- Favicon: ein Monitorsymbol wie in der Kopfzeile. `setFav()` erzeugt es als `data:` abhängig von `prefers-color-scheme` (schwarz im hellen, weiß im dunklen Design) und aktualisiert es, wenn sich das System ändert. Verwende kein `media` an Symbol-Links: Browser wenden es nicht zuverlässig an.
- Tasten in den Hinweisen werden mit `<kbd>` geschrieben (Klassen `r` für Fernbedienung und `g` für Gamepad), damit sie in einem Kasten erscheinen.
- Die räumliche Navigation (`spatial`) wird nur aktiv, wenn ein Element den Fokus hat (Tastatur und Maus) oder immer (Fernbedienung und Gamepad), damit Tastaturnutzer das Scrollen mit den Pfeiltasten behalten.

## Sicherheitsregeln

- Keine Lichtblitze und kein automatisches Flackern. Bewegung bleibt moderat, und der Hinweis zur Photosensitivität muss sichtbar bleiben.
- Die Geschwindigkeit beim Ghosting ist auf 2–6 s pro Durchgang begrenzt. Nicht unter 2 s gehen.
- Der Pixel-Entsperrer startet pausiert. Jedes Feld wechselt zufällig und eigenständig seine Farbe, mit einem mittleren Intervall von 10 s bis 0,1 s (Geschwindigkeit 1–16) und ±40 % Abweichung; die Felder werden neu geplant, wenn sich die Geschwindigkeit ändert, damit sie nie gemeinsam wechseln. Ab 3 Wechseln pro Sekunde (Geschwindigkeit 13 oder mehr) werden mindestens 8 Spalten erzwungen, damit das Flackern sich nicht auf wenige Felder konzentriert, und die Beschriftung zeigt „schnell“. Entferne diese Grenze nicht und erhöhe die Geschwindigkeit nicht, ohne den Projektverantwortlichen zu informieren.
- Der Smearing-Test (VA) startet pausiert und zeigt den Hinweis zur Photosensitivität.
- Die Bedienelemente der Ansicht müssen sich ausblenden lassen, damit Gleichmäßigkeitstests nicht verfälscht werden.

## Einen Test hinzufügen

1. Füge ein Objekt zu `TOOLS` hinzu mit `id`, `name`, `cat`, `desc`, `p` (Standardparameter), `ctl` (Bedienelemente, optional) und `draw(p, W, H, live)`, das das SVG zurückgibt. Ist er animiert, verwende `kind:"cv"` mit `init`, `frame` und `thumb`.
2. Handelt es sich um eine neue Kategorie, füge sie zu `CATS` hinzu.
3. Bedienelemente können `range` (`min`, `max`, `step`, `fmt`), `choice` (`opts`), `preset` (Kurzwahl auf einen Wert) oder `play` (Starten und Pausieren) sein.
4. Füge jeden sichtbaren spanischen Text in allen Sprachen von `DICT` hinzu und aktualisiere die Werkzeugtabelle in `README.md` und den Übersetzungen.
5. Prüfe die Website mit der oben genannten Testliste.

## Commits

Kurze Nachrichten auf Spanisch oder Englisch, im Imperativ, mit einer Zusammenfassungszeile. Möglichst eine Änderung pro Commit.
