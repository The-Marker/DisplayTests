[English](README.md) · [Español](README.es.md) · [Português](README.pt.md) · [Français](README.fr.md) · **Deutsch**

# DisplayTests

Eine Website mit Werkzeugen zum Testen und Diagnostizieren von Bildschirmen an Handys, Computern und Fernsehern. Sie besteht aus einer einzigen Datei, `index.html`, ohne Abhängigkeiten und ohne Build-Schritt.

## Verwendung

Öffnen Sie `index.html` in einem Browser (Doppelklick) oder veröffentlichen Sie die Datei auf einem beliebigen statischen Hosting, zum Beispiel GitHub Pages. Tippen Sie auf eine Miniatur, um den Test im Vollbild zu öffnen.

Stellen Sie zum Messen die Helligkeit des Bildschirms ein, verwenden Sie Vollbild und bei den Schwarztests einen dunklen Raum. Die angezeigten Farben sind eine Näherung.

## Highlights

**Testwerkzeuge**

| Test | Kategorie | Wofür er da ist |
| --- | --- | --- |
| SMPTE-Balken | Farbe | Farbe, Helligkeit und Schwarzwerte prüfen |
| Farb- und Graustufenskalen | Farbe | Graustufenverlauf und sechs Farbskalen mit zehn Stufen (Rot, Grün, Blau, Cyan, Magenta und Gelb). Mit der Option Skalierung siehst du alle oder nur eine |
| Tiefe Schwarztöne | Farbe | Balken von 0 bis 8 % auf Schwarz, um zu sehen, ob der Fernseher Schatten abschneidet oder Schwarz anhebt (dunkler Raum) |
| Spitzenhelligkeit | Farbe | Weißes Fenster von 10 bis 100 % der Fläche auf Schwarz, zur Messung der Spitzenhelligkeit; SDR- oder HDR-Bereich. HDR braucht einen kompatiblen Browser und Bildschirm, und die Ansicht erklärt, wie man es aktiviert |
| Kontrast | Farbe | Blöcke von 5 % bis 95 % mit einstellbarer Stufe |
| Graue Gleichmäßigkeit | Gleichmäßigkeit | Grau von 0 bis 100 % mit Kurzwahl für Schwarz und Weiß: Flecken, Vignettierung, Lichtlecks, Wolken und Banding |
| RGB- und CMYK-Gleichmäßigkeit | Gleichmäßigkeit | Immer eine Vollbildfarbe: Rot, Grün, Blau, Cyan, Magenta, Gelb, Weiß und Schwarz, von Hand gewählt. Auch geeignet, um tote Pixel zu finden |
| Berührungszähler | Touch | Ein nummerierter, farbiger Kreis pro Berührungspunkt; die Kreise bleiben nach dem Loslassen und werden beim erneuten Berühren gelöscht. Zählt gleichzeitige Berührungen und das Maximum |
| Wischraster | Touch | Einstellbares Raster, das die Felder ausmalt, die Finger oder Maus überqueren, mit dem bedeckten Anteil in Prozent |
| Pixel-Entstopper | Pixel | Adaptives quadratisches Raster, dessen Felder zufällig zwischen RGB, CMYK, Weiß und Schwarz wechseln, jedes in eigenem Takt; Größe (4–25 % der Breite) und Geschwindigkeit (1–16, von alle 10 s bis alle 0,1 s) einstellbar |
| Lokales Dimming | Bewegung | Sterne verschiedener Größe, die über Schwarz wandern, um Halos und lokales Dimming zu erkennen; Geschwindigkeit, Dichte und Sternengröße einstellbar |
| Ghosting und Smearing | Bewegung | Wähle einen Modus. Ghosting: ein Block überquert den Bildschirm, um Schlieren durch langsame Reaktion zu zeigen (Durchgang von 2 bis 6 s). Smearing (VA): ein weißer Balken hinterlässt auf VA-Panels eine dunkle oder helle Spur; Geschwindigkeit und Hintergrund einstellbar |
| Bewegter Text | Bewegung | Textzeilen, die in gegensätzliche Richtungen laufen, waagerecht oder senkrecht, mit einheitlicher oder gemischter Größe; vergleiche die Schärfe im Stillstand und in Bewegung |
| Geometrie | Schärfe | Raster, oder Kalibrierung mit einem zentralen Kasten im Kreis, der SMPTE-Balken, Graustufen, RGB- und CMYK-Skalen und Kontrast vereint und Auflösung, Dichte und Maßstab des Bildschirms zeigt; mit eingegebener Diagonale berechnet er die ppi |
| Konvergenz | Schärfe | Rote, grüne und blaue Raster, mit Punkten nahe den Ecken jedes Feldes; Versatz zeigt sich als farbige Ränder oder Punkte. Für Röhrenbildschirme und Drei-Panel-Projektoren; flache Einzelpanel-Displays sind werkseitig konvergiert |
| Seitenverhältnis und Overscan | Schärfe | Modus: Kreis und Rahmen für 4:3, 16:9, 21:9 und 32:9, jeder am nächsten Rand anliegend und benannt; oder Overscan, mit Rahmen bei 0, 2, 5 und 10 % vom Rand, um zu sehen, ob das Bild beschnitten wird (vor allem bei Fernsehern) |
| Quadratische Felder | Schärfe | Schachbrett aus Quadraten; rechteckige Felder zeigen ungleiche Skalierung |
| Feine Linien | Schärfe | Linien mit genau einem Pixel, um Skalierung, Unschärfe und Moiré zu erkennen |
| Textschärfe | Schärfe | Text in vielen Größen, mit Serifen, nichtproportional und farbig, auf Weiß und auf Schwarz, um die Schärfe auf Bildschirmen mit weißem Subpixel (z. B. W-OLED) zu prüfen |

**Website**

- **Responsiv:** 2 Spalten auf dem Handy, 3 auf Tablets, 4 auf dem Computer und 5 auf Fernsehern mit größerer Schrift. Die Filter sind auf jeder Bildschirmgröße eine Reihe von Schaltflächen, wie auf dem Handy. Kopfzeile, Hinweis zur Photosensitivität und Filter bleiben beim Scrollen oben.
- **Vollbild-Ansicht:** Jeder Test passt sich dem tatsächlichen Seitenverhältnis des Bildschirms an. Die Bedienelemente werden mit `H` oder einem Mausklick ein- und ausgeblendet (auf Touchscreens mit Doppeltipp) und verschwinden außerdem nach 5 Sekunden ohne Eingabe von selbst, damit Gleichmäßigkeitstests nicht verfälscht werden. Mausbewegung blendet sie nicht ein.
- **Mehrere Eingaben:** Tastatur, Maus, Touchscreens, Fernbedienungen, Gamepads und Joysticks. Die Bedienhinweise in der Ansicht passen sich der erkannten Eingabe an, und Tasten werden in einem Kasten angezeigt, damit sie auffallen. Siehe Abschnitt Bedienung.
- **Automatisches Design:** folgt dem hellen oder dunklen Modus des Systems auf Android, iPhone, Windows, macOS und Linux. Ist das System dunkel, wird das graue dunkle Design verwendet, oder reines Schwarz, wenn du die Option im Designmenü aktivierst. Meldet das Gerät nichts, wird das helle Design verwendet.
- **Designmenü:** Ein einzelnes Symbol in der Kopfzeile öffnet ein Menü mit Automatisch, Hell, Dunkel und Reines Schwarz; das Symbol zeigt den aktuellen Zustand. Hell, Dunkel und Reines Schwarz legen das Design fest und schalten die Systemerkennung aus. Darunter macht das Kästchen **Reines Schwarz im dunklen Modus verwenden** aus dem dunklen Design reines Schwarz, besonders geeignet für OLED-Bildschirme. Die Einstellung wird im Browser gespeichert.
- **Kopfzeile:** Link zu GitHub, eine Schaltfläche, die den automatischen Start von Bewegungstests ein- und ausschaltet (standardmäßig aus; die Wahl wird gespeichert), sowie die Menüs für Design und Sprache.
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
| Bedienfeld ein- oder ausblenden | `H` | Bildschirm anklicken (Touch: Doppeltipp) | `OK` oder `Info` | `Start` |
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
