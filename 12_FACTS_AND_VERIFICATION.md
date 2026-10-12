# 12 · Facts, confidence and game updates
Use for: keeping the planner true to the game after a patch; how sure we are of each number and rule; how to check quickly without testing everything in game.
Read with 01. Add the topic doc when a rule needs code (03 threat, 04 protection, 05 haul, 11 structures). Fact sheet storage: doc 06.

**Status (12 Oct 2026): proposal.** Nothing here is built yet. Parts marked **Code** need Claude to change the page; parts marked **Admin** you can do in the Fact sheet today or once the code is in.

## 0. In short
1. Every fact gets four things: **value, confidence, date, source**. Plus the game version it was checked on.
2. Confidence is a number from a fixed scale (10 Guess … 100 Confirmed by tester). Players only see it when they hover; the sheet looks as today.
3. A patch never changes confidence by itself. It marks facts in the touched areas as **"not checked since patch X"**.
4. After a patch: read the notes → fill one patch file → update what the notes state → check the rest with cheap sources → test in game only what is important **and** still doubtful.
5. Fast checks without the game: a small set of **reference designs** whose threat, haul and build answers we know. Open them after every change and compare.

---

## 1. One fact

| Field | Example | Notes |
|---|---|---|
| ID | `stack` | The key the code uses (`WD.F('stack')`). Never changes. |
| Fact | Supplies per stack / crate slot | The label on the Fact sheet. |
| Value | 50 | Whole number within its limits (as today). |
| Confidence | 100 · Confirmed by tester | From the scale below. |
| Date | 2026-10-12 | The day it was last **confirmed at that level**, not the day it was typed in. |
| Source | "Crate test, 2 Oct" or a link | Short text; a link when there is one. |
| Patch | 0.11 | Game version it was checked on (as Steam shows it). |
| Area | Logistics | Used to mark facts after a patch (list in §1.3). |

Written short, as you asked:
```
Fact: "Supplies per stack / crate slot", 50, Confirmed (100), 2026-10-12, patch 0.11, source: crate test
```

### 1.1 Confidence scale

| Level | Name | What it takes | Shown to players on hover |
|---|---|---|---|
| 10 | Guess | Nobody has a source. A placeholder so the planner can work. | Guess |
| 30 | Best guess | Worked out from other facts or from a similar piece (e.g. Drill Rig build time from supplies, Corner HESCO = Large HESCO C4). | Best guess |
| 50 | 3rd party source | Guide sites, datamine, wiki, Reddit, YouTube. | From a guide / datamine |
| 70 | Dev logs | Official patch notes, Steam news, a developer's own post. | From the patch notes |
| 90 | Confirmed by user | A player saw it in the game once: a screenshot, a clip, a comment from a friend. | Seen in game |
| 100 | Confirmed by tester | You or a listed tester tested it on purpose: method written down, result recorded, screenshot. | Tested in game |

My reading of 90 vs 100 (change it if you meant something else): **90 = seen**, **100 = measured on purpose**. That keeps "a friend said the gate takes 2 C4" apart from "we blew three gates and it was 2 every time".

Rules for using the scale:
- **The best source wins.** Keep the value with the highest confidence. If a lower source disagrees, add it to the note ("Skycoach says 12") and put the fact on the check list.
- **Dev logs (70) beat a test (100) from before that patch.** If the patch notes give a new number, take it at 70 with today's date; it goes back to 100 when someone tests it.
- **Guesses must be honest.** A rule the code needs but nobody knows gets 10, not a nicer number. Low numbers are what make the to-test list.
- **Bug-dependent** facts get a tag (`bug`). Example: `rule.ladderStruct`, the ladder quirk. These are the first to check after every patch, because "fixed X" in the notes can kill them.

### 1.2 Starting values for what's on the sheet today
One-time job (**Code**, Claude does it from the notes already in the code):

| Today's note says | Starts at |
|---|---|
| "Tested in game", "Checked in game", "Timed in game" + date | 100, that date |
| Your game answers in docs 03/11 (collapse tests 10 Oct, C4 blast 10 Oct, sandbags 12 Oct) | 100, that date |
| "Some guides say …" | 50 |
| No note, figure from Dakanoth / wardogshub.gg / AllThings.How / Skycoach / wardogs.tools | 50, date 2026-09-10 (Season 1 sources) |
| "Estimate" tick (`est`), or "guessed from …" | 30 |
| "assumed", "a guess", Planner rules marked "?" in doc 11 | 10 |

Claude lists every fact with the level it picked so you can correct them in one go.

### 1.3 Areas
Patch notes are written per game system, so facts are grouped the same way:
**Building** (costs, hammer tiers, build times, stacking, FOB area) · **Structures** (blueprints, collapse) · **C4 and damage** · **Movement** (jumps, climbing, vehicles' reach) · **Weapons** (emplacement ammo, angles, range) · **Logistics** (crates, pallets, vehicles, prices, levels, unloading).
Today's Fact sheet groups map onto these one to one or two to one; the threat-check rules (§2) get an area each.

---

## 2. Four kinds of facts, and who can edit them

| Kind | Examples | Where it lives today | You edit the value | You edit confidence, date, source |
|---|---|---|---|---|
| **A · Numbers on the Fact sheet** | stack size, C4 per piece, heights, build times | Fact sheet (`wd-facts`) + Firebase `facts/main` | **Admin**, already works | **Code** once (step 1), then Admin |
| **B · Numbers hidden inside rules** | 3×3 C4 blast, collapse at "half" the ground HESCO, roof falls at "2" corners, Corner HESCO 1.65 high, max 1 Refuel + 1 Repair per FOB, 1-square gap round emplacements | In the code | **Code** once to move each onto the Fact sheet (step 3), then Admin | Same |
| **C · Shapes** | Structure blueprints (Recon, Shelter, Bunker), piece footprints, roof shapes | Built-in blueprints in code (`BUILTIN_BP`); your own structures in the Structure designer | Built-in: **Code**. Own structures: Admin via Structure designer | **Code** once: one confidence per blueprint, plus "?" per block where unsure (the "?" on piece names already exists) |
| **D · Behaviour rules** | how jumps work, what can be walked through, vehicles only on open ground, Bremer covers an opening, ladder foot is kept free | In the code; written out read-only under "Movement and threat rules" | Always **Code** | **Code** once (step 2), then Admin |

The idea for D: the rule itself needs Claude, but **how sure we are** of it does not. Each rule line under "Movement and threat rules" gets an ID and the same confidence / date / source as a number. Then you can mark "Bremer face rule: 90, 2026-10-14, Discord clip" yourself, and a low-confidence rule shows up on the to-test list next to the numbers.

### 2.1 Rule register (kinds B and D), first draft
IDs Claude would give the rule lines. Levels are my suggestion from what the docs say; **?** = you know better, set it.

| ID | Rule | Kind | Area | Suggested | Why |
|---|---|---|---|---|---|
| `r.c4.blast` | One charge takes every block in the 3×3 around it | B | C4 | 100 · 2026-10-10 | HESCO test (doc 11 §6.2) |
| `r.c4.blast.struct` | Same blast on structure blocks | D | C4 | 90 | "Snurra says structures behave the same", not measured |
| `r.c4.blast.up` | Blast doesn't reach blocks stacked on top (H2+) | D | C4 | 30 | Planner's guess, open question |
| `r.c4.sandbag` | 1 C4 on sandbags takes the HESCO next to them | D | C4 | 100 · 2026-10-12 | Your test |
| `c4.corner` *(new number)* | C4 to blow a Corner HESCO = 4 | B | C4 | 10 | Copied from Large HESCO |
| `c4.window` | 1 C4 opens a window | A | C4 | 30 | Open question (doc 11 Q5) |
| `r.collapse.count` | Floor/roof on the ground ring falls at half the original ground HESCO | B | Structures | 100 · 2026-10-10 | Recon + Shelter tests |
| `r.collapse.corner` | Roof on corner HESCO falls when 2 corners are gone | B | Structures | 100 · 2026-10-10 | Recon + Bunker tests |
| `r.collapse.original` | Only original blocks hold anything up | D | Structures | 100 · 2026-10-10 | Shelter tests 3, 3b |
| `r.collapse.onTop` | Pieces you built on a roof fall with it | D | Structures | 30 | Planner says yes, unchecked |
| `r.headroom` | No Large HESCO or Door under a roof on corner HESCO (1.65) | B | Structures | 90 | Fixed from your report |
| `r.entrance.h` | Entrance opening is Door height (H2) | D | Movement | 30 | H2 rule vs 1.4 in Side view, open |
| `r.walkthru` | Wire, hedgehogs, tents, speakers, radios, emplacements, stations don't block | D | Movement | ? | |
| `r.jump` | Jump rules (1-gap up 1, 2-gap level, no squeezing past corners) | D | Movement | ? | |
| `r.vehicle.ground` | Vehicles drive only on open ground | D | Movement | ? | |
| `r.bremer.cover` | Bremer outside an opening, face in, covers it | D | Movement | ? | |
| `r.ladder.foot` | Nothing on a ladder's foot square | D | Building | ? | |
| `rule.ladderStruct` | Structures may block a ladder (game quirk) | A · `bug` | Building | 90 | Likely a bug: recheck every patch |
| `r.fob.stations` | Max one Refuel and one Repair Station per FOB | B | Building | ? | |
| `r.elevation` | Free foundation from a piece on small HESCO, chains | D | Building | ? | |
| `r.gap` | 1-square gap round emplacements (switched off) | B | Building | ? | To-do: decide keep or delete |

The open questions in `09_TODO.md` → "Check in the game" are exactly the 10s and 30s here. Once this is built, that list can be read straight off the Fact sheet instead of kept by hand (ask before I change 09).

---

## 3. How it looks

**Players** (sheet as today):
- Hover a value or a rule line → `Tested in game · 12 Oct 2026 · patch 0.11` and the source on a second line.
- "Estimate" is no longer ticked by hand: it shows by itself for confidence 30 and below.
- When the fact is older than the last patch that touched its area: a small `not checked since 0.12` after the label.
- "Copy sheet as text" adds confidence and date to each line.

**You as admin** (one row on the sheet):
```
Supplies per stack / crate slot     [ 50 ]  [Confirmed by tester ▾]  [2026-10-12]  [patch 0.11]  source: [crate test, 2 Oct]
```
- Change a value → confidence and date ask to be set (date fills in today; confidence keeps the last level you used).
- "Mark checked" button: same value, new date and patch, in one click. This is the common case after a patch.
- Top of the sheet: **Game version the sheet is checked against** + a small **Patches** list (version, date, areas it touched). Adding a patch here is what turns on the "not checked since" marks.
- Filter: "Show only: below 50 · not checked since last patch · bug-dependent". That filter is your to-do list after a patch.

---

## 4. Code needed (in order, each can go on test by itself)

| Step | What | Size | Firebase rules |
|---|---|---|---|
| 1 | Confidence, date, source, patch per Fact sheet number; starting levels from §1.2; hover text; admin editing | Medium | **Yes**: `facts/main` and `test_facts/main` get a `meta` field next to `values` (doc 06: any new stored field needs a rules change). Claude gives you the exact steps. |
| 2 | IDs on the rule lines; confidence etc. per rule (same storage as step 1); filter | Small after step 1 | Same as step 1 |
| 3 | Move the kind-B numbers onto the sheet (blast size, collapse half, corner count, corner HESCO height and C4, stations per FOB, gap) | Medium; touches threat check (doc 03) and structures (doc 11) | No |
| 4 | Patches list + "not checked since" marks + "Mark checked" | Small | Yes, same field as step 1 |
| 5 | **Paste updates** (admin): paste a list of changes Claude prepared from patch notes, see old → new side by side, tick what to apply | Small | No |
| 6 | Reference designs check (§6): one button for admin, or a Claude test run | Small–medium | No |
| 7 | One confidence per built-in blueprint, "?" per unsure block | Small | No |

Step 1 + 4 + 5 give most of the value. 3 matters most for the threat check after a big patch.

---

## 5. When a game update comes

### 5.1 Notice it
| Where | Why |
|---|---|
| Steam news for WARDOGS — https://store.steampowered.com/news/app/1867240 | The official patch notes. Follow the game on Steam to get them. |
| Steam RSS feed — https://store.steampowered.com/feeds/news/app/1867240/ | Same, as a feed (phone, Discord bot, or a scheduled check by Claude). |
| SteamDB patch history — https://steamdb.info/app/1867240/patchnotes/ | Shows **every** build, also silent hotfixes without notes. A build with no notes = check the `bug` facts. |
| The official WARDOGS Discord (invite on the Steam page) | Patch notes, hotfix announcements, known-issues posts, dev answers (70). |

### 5.2 The steps

**1. Collect (15 min).** Official notes first. Then wait a day or two and look at the datamine and the community; they catch numbers the notes don't give.

**2. Fill a patch file** `PATCH_<version>.md` (template in §5.4). Each line of the notes → area → which fact IDs → one action:
- **Update**: the notes give the new number → set it, confidence 70, today, source = notes.
- **Check**: the notes are vague ("rebalanced HESCO", "improved structure collapse") → leave the value, it gets the "not checked since" mark, goes on the check list.
- **New**: new building, vehicle, piece → add facts at 10–50; new structure → Structure designer first (doc 11 §10 Q11: name, size, 1–2 photos).
- **Ignore**: nothing the planner uses (UI, audio, cosmetics).
Always add to Check: every `bug` fact, and anything the notes call a fix in the same area (a "fixed exploit" may be a quirk the planner models).

Claude can do step 2 for you in a short chat (01 + 12, Sonnet): paste the notes, get the filled patch file and a "Paste updates" list back.

**3. Check cheaply, in this order, before going to the game:**
1. Patch notes say the number → 70, done.
2. Datamine updated after the patch (wardogs.tools) agrees → keep 70, add it to the source. Disagrees → note both, put on test list.
3. Guides / Reddit / clips → 50; useful to know *what* changed when the notes are vague.
4. Ask a friend or tester to look at one thing while they play anyway → 90.
5. Planned test session → 100.

**4. Decide what to test in the game.**
Importance:
- **High**: changes what the threat check says (C4, collapse, movement, heights, walk-through), or whether a piece may be placed (stacking, footprints, FOB area).
- **Medium**: haul, build time, build supplies.
- **Low**: prices, levels, unlock fees.

Test in game only if **High and below 90**, or **sources disagree** on a High one. Everything else waits until someone happens to see it. Batch all of it into one session with a filled-in questionnaire (cheat sheet habit 7): "Fact, what the planner says, what you saw, photo".

**5. Update the planner.**
- Numbers: on **test** first (test reads `test_facts/main`), open the reference designs, then the same edits on **live**. With step 5 of the code this is one paste each.
- Rules that need code: one chat, 01 + 12 + topic doc, "rule `r.xxx` changed in patch X: …".
- "Mark checked" on what you confirmed unchanged.

**6. Close.** Patch file → "Done". Release notes get one line: "Facts checked against patch X." Update the game version at the top of the sheet.

### 5.3 Sources and what they are worth

| Source | Use it for | Confidence | Link |
|---|---|---|---|
| Your own tests, listed testers | anything High | 100 | doc 11 §10, `09_TODO.md` |
| A friend's screenshot or clip | quick confirmation | 90 | — |
| Steam news / official patch notes | what changed, stated numbers | 70 | https://store.steampowered.com/news/app/1867240 |
| Official Discord, dev posts | hotfixes, known issues, dev answers | 70 | invite on the Steam page |
| wardogs.tools database (datamine) | costs, footprints, numbers the notes skip | 50 | https://wardogs.tools/database/buildables |
| Dakanoth | FOB, hammers, crates, vehicles | 50 | https://dakanoth.com/wardogs/ |
| wardogshub.gg | logistics | 50 | https://wardogshub.gg/blog/wardogs-logistics-guide/ |
| AllThings.How, Skycoach | build costs | 50 | already in Fact sheet → Sources |
| Patch-note mirrors (Dexerto wiki, Prima Games, BisectHosting blog) | backup when Steam is hard to search; check they quote the official text | 50 (70 if a word-for-word copy) | https://www.dexerto.com/wikis/wardogs/patch-notes/ |
| Reddit, Steam discussions, YouTube | bugs, quirks, "what does *improved* mean" | 50 | — |

Guide sites lag behind patches: always look at the article date. Anything dated before the patch is about the old game.

### 5.4 Patch file template
```
# Patch <version> · <date> · <link to notes>
Status: Collecting / Checking / Done

| Note line (short) | Area | Fact IDs | Action | New value | Conf | Done |
|---|---|---|---|---|---|---|
| HESCO Large cost 14 → 16 | Building | b.hesco_l | Update | 16 | 70 | [ ] |
| Improved structure collapse | Structures | r.collapse.* | Check | | | [ ] |
| Fixed placing over ladders | Building | rule.ladderStruct (bug) | Check | | | [ ] |

## Test in game (High and below 90 only)
- [ ] r.collapse.count: blow 5 of the 10 Recon ground HESCO; does floor 2 fall? Photo.

## Silent builds since (SteamDB)
- <date> build <id>: checked bug facts [ ]
```

---

## 6. Fast checks without the game: reference designs
Most fact or rule changes show up in a few answers the planner gives. Keep **5–8 small saved designs** whose answers you know, each written down once:

| Design | What it checks | Expected |
|---|---|---|
| 2-layer HESCO wall round a mortar | C4 per layer, blast doesn't take the 2nd layer | C4 route = … |
| Bunker on the ground, entrance sealed | corner rule, window C4 | … |
| Recon with 5 ground HESCO removed | count rule collapse | floor 2 down |
| Bremer line, faces out, one turned | Bremer sneak rule | on foot gets in at … |
| Car-height wall (H3) vs H4 | car / Ural reach | car gets in / Ural gets in |
| Small base, full haul | crates, pallets, trips | Ural trips = … |
| Mortar with sandbags 1 out | protection angle, range | 685 m |

After any change (a patch's facts, or new code): open each, compare. Something moved that shouldn't → look before release. Claude can run all of them in the Playwright test in one go (code step 6), so "Put it on test" also says "reference designs: all as expected" or lists the difference.

When a patch really changes an answer (e.g. C4 per HESCO goes up), update the expected value in this table in the same commit.

---

## 7. Keeping a history
- The page keeps one current value per fact (+ its date).
- History comes from the repo: at each release, Claude saves the "Copy sheet as text" output as `facts_<date>.txt` (needs a small addition to doc 08; ask first). Comparing two of those shows what changed between patches.
- Patch files stay in the repo after "Done".
