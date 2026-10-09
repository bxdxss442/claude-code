# Ragdoll Arena

Übernommen aus dem claude.ai-Artefakt „Ragdoll Arena“
(https://claude.ai/artifact/NVA7cPY6B9PwpQZU3g4tre, Stand 2026-10-08)
und vollständig ins Englische übersetzt (UI, Moves, Items, Dialoge,
Regeln, KI-Prompts). Code-Kommentare sind noch auf Deutsch.

- `index.html` – das komplette Spiel als eine Datei (HTML, CSS, JS inline).
- Lokal starten: `index.html` im Browser öffnen oder
  `python3 -m http.server` in diesem Ordner ausführen.
- Die Artefakt-Laufzeitfunktionen (`window.claude`: KI-Dialoge, gemeinsame
  Datenbank, Nutzer) gibt es nur auf claude.ai; lokal fällt der Code
  stillschweigend darauf zurück, ohne sie zu laufen.

## Character Creator (Second Selection)

Über „🛠 Character Creator“ in der Second-Selection-Übersicht (oder „🛠 New
character“ in der Favoriten-Ansicht des Kaders) baut man eigene Kämpfer:
Name, Körperbasis, Ego-Typ, Rolle, die fünf Werte, drei Techniken + Ultimate,
Farben, Extras, Skins, Fluchgegenstände und Begleiter. Gespeichert wird in der
Favoriten-Bibliothek; „Save & insert“ ersetzt einen Kämpfer des laufenden
Turniers, über „Neue Saison“ lassen sich die Figuren ebenfalls importieren.
