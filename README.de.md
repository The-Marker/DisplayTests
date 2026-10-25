[English](README.md) · [Español](README.es.md) · [Português](README.pt.md) · [Français](README.fr.md) · **Deutsch**

# DisplayTests

Eine Website mit Werkzeugen zum Testen und Diagnostizieren von Bildschirmen an Handys, Computern und Fernsehern. Sie besteht aus einer einzigen Datei, `index.html`, ohne Abhängigkeiten und ohne Build-Schritt.

## Verwendung

Öffnen Sie `index.html` in einem Browser (Doppelklick) oder veröffentlichen Sie die Datei auf einem beliebigen statischen Hosting, zum Beispiel GitHub Pages. Tippen Sie auf eine Miniatur, um den Test im Vollbild zu öffnen.

Stellen Sie zum Messen die Helligkeit des Bildschirms ein, verwenden Sie Vollbild und bei den Schwarztests einen dunklen Raum. Die angezeigten Farben sind eine Näherung.

## Highlights

**Testwerkzeuge**

| Werkzeug | Kategorie | Wofür es dient |
| --- | --- | --- |
| SMPTE-Balken | Farbe | Farbe, Helligkeit und Schwarzwerte prüfen |
| Graustufen | Farbe | Prüfen, ob sich dunkle und helle Töne unterscheiden lassen |
| Tiefe Schwarztöne | Farbe | Balken von 0 bis 8 % auf Schwarz, um zu sehen, ob der Fernseher Schatten abschneidet oder Schwarz anhebt (dunkler Raum) |
| RGB- und CMYK-Skala | Farbe | Sechs Skalen mit zehn Stufen, je eine pro Farbe (Rot, Grün, Blau, Cyan, Magenta und Gelb). Mit der Option Skala zeigen Sie alle oder nur eine an |
| Spitzenhelligkeit | Farbe | Weißes Fenster von 10 bis 100 % der Fläche auf Schwarz, zur Messung der Spitzenhelligkeit; SDR- oder HDR-Bereich (HDR nur, wenn Browser und Bildschirm es unterstützen) |
| Kontrast | Farbe | Blöcke von 5 % bis 95 % mit einstellbarer Stufe |
| Graue Gleichmäßigkeit | Gleichmäßigkeit | Grau von 0 bis 100 % mit Kurzwahl für Schwarz und Weiß: Flecken, Vignettierung, Lichtlecks, Wolken und Banding |
| RGB- und CMYK-Gleichmäßigkeit | Gleichmäßigkeit | Immer eine Vollbildfarbe: Rot, Grün, Blau, Cyan, Magenta, Gelb, Weiß und Schwarz, von Hand gewählt. Auch geeignet, um tote Pixel zu finden |
| Berührungszähler | Touch | Ein farbiger Kreis pro Berührungspunkt; die Kreise bleiben nach dem Loslassen und werden gelöscht, wenn der Bildschirm erneut berührt wird. Zählt gleichzeitige Berührungen und das Maximum |
| Wischraster | Touch | Einstellbares Raster, das die vom Finger oder von der Maus überquerten Felder einfärbt, mit dem abgedeckten Prozentsatz |
| Pixel-Entstopper | Pixel | Adaptives quadratisches Raster, dessen Felder zufällig zwischen RGB, CMYK, Weiß und Schwarz wechseln, jedes in eigenem Takt; Größe (4–25 % der Breite) und Geschwindigkeit (1–16, von alle 10 s bis alle 0,1 s) einstellbar |
| Local Dimming | Bewegung | Sterne verschiedener Größe, die über Schwarz wandern, um Halos und lokales Dimming zu erkennen; Geschwindigkeit und Dichte einstellbar |
| Smearing (VA) | Bewegung | Ein weißer Balken wandert über dunkle Hintergründe, um die dunkle oder helle Spur von VA-Panels zu zeigen; Geschwindigkeit und Hintergrund einstellbar, mit Pause |
| Ghosting | Bewegung | Spuren durch langsame Reaktionszeit; Durchgang von 2 bis 6 s |
| Overscan und Ränder | Schärfe | Rahmen bei 0, 2, 5 und 10 % vom Rand, um zu sehen, ob das Bild beschnitten wird (vor allem bei Fernsehern) |
| Feine Linien | Schärfe | Linien mit einem echten Pixel, um Skalierung, Unschärfe und Moiré zu erkennen |
| Geometrie | Schärfe | Raster, Kreis und Diagonalen für Proportionen und Schärfe |
| Geometrie und Kalibrierung | Schärfe | Dasselbe, mit einem zentralen Feld im Kreis, das SMPTE-Balken, Graustufen, RGB- und CMYK-Skala sowie Kontrast vereint und Auflösung, Dichte und Skalierung des Bildschirms anzeigt; mit eingegebener Diagonale berechnet es die ppi |

**Website**

- **Responsiv:** 2 Spalten auf dem Handy, 3 auf Tablets, 4 auf dem Computer mit Filtern in einer Seitenleiste und 5 auf Fernsehern mit größerer Schrift.
- **Vollbild-Ansicht:** Jeder Test passt sich dem tatsächlichen Seitenverhältnis des Bildschirms an. Die Bedienelemente werden mit `H` oder durch Tippen auf den Bildschirm ausgeblendet, damit Gleichmäßigkeitstests nicht verfälscht werden.
- **Mehrere Eingaben:** Tastatur, Maus, Touchscreens, Fernbedienungen, Gamepads und Joysticks. Die Bedienhinweise in der Ansicht passen sich der erkannten Eingabe an, und Tasten werden in einem Kasten angezeigt, damit sie auffallen. Siehe Abschnitt Bedienung.
- **Automatisches Design:** folgt dem hellen oder dunklen Modus des Systems auf Android, iPhone, Windows, macOS und Linux. Ist das System dunkel, wird reines Schwarz verwendet, das sich besonders für OLED-Bildschirme eignet. Meldet das Gerät nichts, wird das helle Design verwendet.
- **Designmenü:** Ein einzelnes Symbol in der Kopfzeile öffnet ein Menü mit Automatisch, Hell, Dunkel und Reines Schwarz; das Symbol zeigt den aktuellen Zustand. Hell, Dunkel und Reines Schwarz legen das Design fest und schalten die Systemerkennung aus. Die Einstellung wird im Browser gespeichert.
- **Sprachen:** Englisch, Spanisch, Portugiesisch, Französisch und Deutsch. Die Sprache wird automatisch anhand der Systemsprache gewählt; ist sie nicht unterstützt oder nicht erkennbar, wird Englisch verwendet. Das Globus-Symbol links neben dem Designsymbol ermöglicht die manuelle Auswahl.
- **Kategoriefilter:** Farbe, Gleichmäßigkeit, Pixel, Bewegung, Schärfe und Touch.
- **Sicherheit:** Hinweis für lichtempfindliche Personen, Bewegung ohne Blitze und ein Pixel-Entstopper, der pausiert startet, mit zufälligen und für jedes Feld unabhängigen Farbwechseln. Ab Geschwindigkeit 13 (mehr als 3 Wechsel pro Sekunde) hat das Raster mindestens 8 Spalten und es erscheint ein Hinweis.

## Bedienung

Die Website erkennt die zuletzt verwendete Eingabe und passt die Hinweise in der Ansicht entsprechend an.

| Aktion | Tastatur | Touch | Fernbedienung | Gamepad oder Joystick |
| --- | --- | --- | --- | --- |
| Test wechseln | `←` `→` | Seitlich wischen, oder Schaltflächen Zurück und Weiter | `◀` `▶`, `CH+` `CH−` | `◀` `▶`, `LB` `RB` |
| Zu den Bedienelementen | `↓` (und `↑` zum Zurückgehen) | Bedienelement antippen | `▼` (und `▲` zum Zurückgehen) | `▼` (und `▲` zum Zurückgehen) |
| Bedienelement einstellen | `←` `→` am Schieberegler | Ziehen | `◀` `▶` | `◀` `▶` oder linker Stick |
| Bedienfeld ein- oder ausblenden | `H` | Bildschirm antippen | `OK` oder `Info` | `Start` |
| Starten oder pausieren | `Leertaste` | Schaltfläche Pausieren/Starten zwischen Zurück und Weiter | `⏯` | `X` |
| Bestätigen | `Enter` | Antippen | `OK` | `A` |
| Schließen | `Esc` | Nach unten wischen | `Zurück` | `B` |

Im Wischraster-Test wechseln Wischgesten weder den Test noch schließen sie die Ansicht, und Antippen blendet das Bedienfeld nicht aus, damit Sie frei malen können. Verwenden Sie in diesem Test die Schaltfläche Schließen, `Esc` oder `H`.

Auf der Startseite bewegen sich Fernbedienungen und Gamepads mit den Pfeiltasten zwischen Schaltflächen, Filtern und Miniaturen (räumliche Navigation). Auf Fernsehern mit Tizen, webOS, Android TV, Fire TV und ähnlichen Systemen startet die Website mit den Hinweisen für die Fernbedienung. Gamepads werden erkannt, sobald Sie eine Taste drücken.

## Kompatibilität

Aktuelle Browser auf Android, iPhone, Windows, macOS und Linux sowie Browser von Smart-TVs mit modernem CSS- und JavaScript-Support.

## Mitarbeit

Siehe [AGENTS.de.md](AGENTS.de.md) für Struktur, Konventionen und das Hinzufügen eines neuen Werkzeugs.

## Lizenz

GNU GPL v3. Siehe [LICENSE](LICENSE).
