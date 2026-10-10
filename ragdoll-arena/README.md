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
- **Wildcard farewell**: Short (about 6 s) and identical for everyone. The fighter stands at a fork like in the manga: slatted corridors branch off, with the pentagon wildcard door on the left and the EXIT door on the right. He looks left and right, then the screen goes black, and he never takes a step in either direction.

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

## Stats with real weight (v61)

| Stat | Curve (20 → 60 → 99) | Traits |
|---|---|---|
| SPD | run speed 0.62 → 1.0 → 1.42×, faster dash | below 40: cannot dash · from 80: afterimages at top speed |
| STR | physical damage 0.62 → 1.5× | from 70: extra knockback · from 85: crushing blows (shockwave, guard break) |
| RES | health 0.7 → 1.45×, stuns 1.35 → 0.6× | below 40: stays down longer · from 80: Iron Body ignores half of all light stuns |
| CE | technique damage 0.65 → 1.45×, cooldowns 1.35 → 0.7×, CE recovery 0.45 → 1.9× | from 85: cursed burst on every technique |
| INT | reaction, reading, mistakes, timing | below 40: misses chances to defend · from 80: reads attacks |

Traits are shown in the fighter view and in the creator.

## 30 new Jujutsu techniques (v62)

| Stat | Techniques |
|---|---|
| CE | Hollow Purple ★5 · Absolute: Ultra Cannon · Wing King · Convergence: Piercing Blood · Auspicious Beasts: Ryu · Disaster Flames · Shikigami Sharks · Sticky Bombs |
| STR | Mahoraga: Sword of Extermination ★5 · Rika: Crushing Grip · Blazing Courage · Rough Energy Barrage · Blood Meteorite |
| SPD | Rika Katana: Draw Cut · Nue · Nyoi Staff: Static Thrust · Tiger Funeral · Manji Kick |
| RES | Insect Armor · Root Prison · Auspicious Beasts: Reiki · Hollow Wicker Basket · Body Repel |
| INT | Domain Amplification · Cursed Corpse Brawlers · Cursed Word: Blast Away! · Space Manipulation: Ui Ui · Heart Catch · Auspicious Beasts: Kaichi · Cursed Word: Run! |

Each technique has its own models and VFX, its own sound layers and its own mechanic (binding, teleporting, stealing CE, reflecting, sealing, delayed bombs, summons and so on). Each also has two upgrade levels, stars and a stat requirement, an element for Chemical Reactions, and an AI rating. Cost and cooldown come from the star balancing. Running tournaments pass every new technique to two suitable fighters.

## Technique variants (v63)

Every technique has **three variants**. Each fighter performs it in one of them. In the tournament the variant is saved with the fighter. In the Character Creator you choose it per technique.

The variants come from a variant engine. While a technique runs, a context attaches to everything it creates (projectiles, summons, areas, beams, delayed effects, buffs, domains) and changes those building blocks:

- **Projectiles:** Seeker (slow, homing) · Lance (fast, straight) · Volley (twice as many, weaker) · Colossus (one giant, slow and devastating)
- **Summons:** Horde (summoned twice, smaller) · Colossus (one giant) · Swift Pack (much faster)
- **Areas, cones, beams:** Wide · Focused · Aftershock (strikes a second time) · Snap (triggers almost instantly)
- **Buffs:** Enduring (lasts longer) · Surge (short, heals on activation) · Shared (the nearest ally gets it too)
- **Close combat and direct techniques:** Swift · Heavy · Twin Strike · Reckless (ultimates only)
- **Domains:** Closed (classic barrier) · Open (no barrier, covers the whole arena, weaker) · Compressed (tiny barrier, brutal sure-hit)

Which building blocks each technique uses was measured automatically (`VAR_USE`); the three variants per technique follow from that. Variants appear in the fighter view, in the creator, on the gacha soul flames, and once per fight above the fighter's head on first use.

## 9:16 vertical mode for short videos (v64)

- **Options (♪) → “9:16 Vertical”** or **F9** switches the whole game into a centered portrait frame (black bars left and right). The setting is remembered.
- The renderer, post-processing, on-screen projection, HUD, cutscene texts and overlays all run inside the frame; `vw` sizes in the CSS are converted to the frame width.
- **Same director as in widescreen, just tighter:** the tournament camera stays on the current duel pair, closer than in widescreen, and turns so the two stand more one behind the other than side by side. That keeps them centered in the narrow frame. If the two are far apart (ranged combat), the camera switches to a close-up of whoever is acting right now, over their shoulder toward the opponent. A gentle fit keeps only the focused fighters in frame; the camera does not zoom out to show everyone. Cinematic letterbox bars are slimmer in this mode.
- **“Clean UI”** or **F10** hides the match buttons and the cutscene skip button so you can record straight away. The ♪ button stays faintly visible in the corner. Pause overlays stay visible.
- For recording, capture the browser window or the centered frame (for example with an OBS crop). A 1080 px tall window gives a 608×1080 frame.

## No time limit, better targeting, scene soundtrack (v65)

- **Fights always go to the end.** The old 150 s limit, which decided by remaining HP, is gone. From 150 s an **OVERTIME** begins: damage rises steadily (+2.5 % per second), and from 210 s the arena drains every fighter equally. A fight therefore always ends by K.O.
- **Better targeting:** fighters no longer ignore an opponent who is hitting them. Taking a hit, or an opponent attacking at close range while your own target is far away, lifts the duel lock right away. Retaliation, threats at close range and opponents nobody is covering get a bonus for every ego. Outside the tournament, the AI also prefers whoever just hit it.
- **Every scene has its own soundtrack** (11 new procedural tracks): Selection Room (lobby), Blue Prison Anthem (tournament intro), Training Grounds (intermission), Face-Off (match intro/lineup), Sudden Death (overtime), Victory Lap (end of a fight), Aftermath (results), Chains (steal/chains/verdict), Farewell (farewells/cut), Crowned (ceremony), Soul Summon (gacha). Fights keep the 6 fight tracks, or the song chosen under Options. Transitions crossfade, and short scenes in the middle of a fight keep the fight music. Options → “Scene music” switches it off.

## Posture, perfect landing, air combos, outnumbered fights, less clutter (v66)

- **No more falling over from your own actions:** if a fighter tips over without having been hit (own move, roll, dash), they catch themselves instead of going ragdoll. Landing from your own jump moves causes no fall damage.
- **Posture:** an extra servo keeps the pelvis and upper body upright as long as a fighter is not ragdolled. Attacks may lean a bit further. In simulations the share of strongly tilted upper bodies (> 0.4 rad, about 23°) dropped from ~50 % to ~10 %.
- **Air combos are back:** the stat and balancing AI had dropped the uppercut and air-follow-up logic. Fighters now use uppercuts again and almost always jump after the target when they have the CE (≈ 3 air combos per fight).
- **Perfect landing:** fighters with high SPD (from 68, up to 60 % at 100) can catch themselves after a launch and land on their feet, with an afterimage and a dust ring.
- **Outnumbered (e.g. 1v2):** nothing is announced, but the outnumbered fighter keeps a chance.
  - The bigger team attacks in turns, mostly the opponent the outnumbered fighter is focusing on, while the others keep their distance and lurk.
  - The outnumbered fighter's combat instinct makes them dodge more often (sometimes with a counter), occasionally break out of combos, recover from stuns faster, and stay on one opponent. Their hits sometimes graze a second opponent.
  - Strength comes about 75 % from stats (INT, RES, SPD before STR, CE) and 25 % from ego.
  - In simulations a fighter of equal strength wins a 1v2 about 23 % of the time (previously 0 %).
  - Visually there is only a subtle, individual aura (embers, mist, flicker, ripples or motes in a personal color) plus breath clouds in a personal rhythm.
- **Less clutter:** hit stars are smaller and appear less often on small hits, and Japanese sound words appear at most every 0.32 s and smaller. In 9:16 mode, only the two fighters in the director's focus show their names, the health bars are narrow, and guard bars and AI labels are hidden.

## Broken figures come back whole, Expert Mode (v67)

- **Repairing figures that fell apart:** a figure that broke into pieces (Lego break) and comes back (revival, plot twist, cutscene) is put back together where it lies: rest pose, all joints recreated. Previously it stayed in pieces.
- **🎓 Expert Mode** (button in the tournament menu, saved with the tournament):
  - Everyone starts with **one basic technique**, the one with the fewest stars.
  - Locked techniques do not exist for the AI, and casts of them are refused.
  - **After every fight**, each participant who has not been eliminated may unlock the next technique. The chance is 34 %, +14 % for a win, plus a little from INT.
  - Unlocks go in ascending order of stars, with the **ultimate last**.
  - **Intermissions** can also awaken a technique. CE meditation, energy flow and forbidden training make it more likely.
  - Every unlock gets the **soul-flame scene from the gacha**. It shows exactly as many flames as are unlocked: the old ones burn in their rarity colours, and the new one appears as a silhouette and is revealed with its card.
  - The scene plays straight after the result scenes of watched matches, and after the intermission for intermission unlocks.
  - Reveals from simulated matches collect under **“🔥 Soul Reveals (n)”**.
  - In simulations, each additional technique adds +4 strength.
  - **Pace scales with tournament size:** unlock chances (matches and intermissions) are multiplied by (120 / fighters)^0.55, which is ×1 at 120 and ≈ ×3 at 16 fighters. Simulated full tournaments:

    | Fighters | Matches in the tournament | Own fights until all 4 techniques (median) | Fighters with all 4 at the end |
    |---|---|---|---|
    | 16 | ~13 | ~2 | ~85 % |
    | 43 | ~23 | ~2 | ~75 % |
    | 120 | ~110 | ~4 | ~60 % |

  - **Wildcard awakening:**
    - Wildcard matches multiply the chance by 2.2.
    - Winners of a wildcard match **always** unlock a technique, with a 50 % chance of a **second** one right after.
    - Losers still get a 20 % chance of a double unlock.
    - Intermissions before wildcard matches multiply the chance by 1.8.
    - The reveal shows “WILDCARD AWAKENING” in gold.
  - The fighter detail view shows 🔥/🔒 for each technique.
