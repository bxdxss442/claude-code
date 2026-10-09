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

## Content Mode, Cutscene Gallery & Repeat Fight (Second Selection)

- **🎬 Content Mode** (button in the tournament menu):
  - **Pause anytime** with ⏸ (top right) or the P key. Fights, finishers and cutscenes freeze.
  - **You pick the steal.** After every steal match, the defeated team is shown in chains and the screens ask "Who will you pick?". Then you return to the menu. Both teams stay locked until you choose under "⛓ Who will you pick?" in the overview.
  - **The pick is announced.** A scene shows "You chose …", followed by either "The rest of the losers team will fall back a stage." or "This means that … will no longer participate in this tournament. LOCK OFF!".
- **🎞 Cutscene Gallery**: Every tournament cutscene is saved together with the tournament state (IndexedDB), so it replays exactly as it first played. You can delete single scenes or reset the whole gallery.
- **↻ Repeat fight** (option in the settings): Rewinds the tournament to before the last match so you can fight it again. It is offered on the result card, in the overview, on the pick screen, and as "↻ Restart" during a fight.
- **Wildcard farewell**: Eliminated fighters walk down a corridor with two doors, EXIT and WILDCARD. The scene cuts away before you see which door they take.

## Gacha Reveal (Character Creator)

"🎰 Gacha reveal" plays a showcase cutscene for a fighter. You can start it from the Character Creator, from favorite cards (🎰 Reveal), or from any fighter's detail view, and replay it as often as you like.

1. **Summoning:** A light orb drops, bursts open, and the fighter appears. The pillar's color shows the overall rarity (R, SR, SSR, UR).
2. **Five training sessions**, one per stat. Each activity has five versions (rank D to S), depending on how good the fighter is at it:
   - **Speed:** sprint course, from tripping over the cones to a lightning dash with a sonic boom.
   - **Strength:** punching bag, from a sore hand to a shattered boulder.
   - **Resistance:** a hail of rocks, from going down after one hit to surviving a boulder from the sky.
   - **Cursed Energy:** aura charge, from fizzling out to an overload pillar.
   - **Intelligence:** a holographic puzzle, from ERROR to "genius in 0.8 s".
   
   Each training ends with the stat counter and a rank stamp.
3. **Stat web** on the big screens: radar chart, OVR, rarity, and the rank for each stat.
4. **Meditation:** Four soul flames appear as silhouettes. One after another they crack open in rarity colors (Common, Rare, Epic, Legendary, Mythic), each with the move name, element, requirement and an explanation. The ultimate comes last.
5. **Finale** in the hall.
