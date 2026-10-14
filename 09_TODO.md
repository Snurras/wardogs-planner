# 09 · To-do list

What's next for the planner, sorted by kind of work. Tick an item (`[x]`) when it's done, then delete it after the next release.
The Base Defender mini-game has its own doc: [10_BASE_DEFENDER.md](10_BASE_DEFENDER.md).

> **QA 10-13 (13 Oct 2026, Claude):** full check of `test.html` against all docs. Every tab, tool, key, the four attacks, Modify structure, Structure designer, Side view, phone width, dark mode and accessibility were tried in a browser (Firebase blocked, so logins, comments and online saving were not tested). No page errors in normal use. Test and live give the same threat, build and haul answers on five reference bases; test is ~10–15 % slower (the 3×3 blast search). New notes are marked *QA 10-13* below. Old items that are already done are marked too, so you can delete them.

## Fix
Things that are wrong or broken and hurt the player directly.

- [x] **Modify Structure** Always show 3 Layers, Change to Ground, Rood, Floor 2. middle. To make it fast as middle is rarely used and Top, Bottom becomes most used for all.
- [x] **Modify Structure** Shows you can get in 2h hesco in bunker/recon top floor. You cant. *Done: no HESCO Large or Door under a roof on corner HESCO (1.65 headroom).*
- [x] *Claude QA* **Threat check: C4 blast and collapse.** One C4 charge takes every block in the 3×3 squares around it (your game test), and blowing enough ground HESCO brings a roof down. The threat check uses neither yet, so C4 counts for thick walls are too high and bases look safer than they are. (doc 03, doc 11 §6)
- [x] *Claude QA* **Side view: show Modify changes.** Blocks added with Modify structure and closed entrances aren't drawn in Side view yet (blocks taken off are). (doc 04)
- [x] *QA 10-13* **One bad design breaks the page for good.** The page keeps your last design in the browser and opens it at start. If that copy has one broken piece (tested: an empty piece), the map, piece list and threat check stay blank on every reload, until the player clears the site's data. Fix: if the stored design can't be read, start with an empty map and say so. (doc 06) *Done: stored copy is cleaned at start; unreadable → empty map + message; staging v155.*
- [x] *QA 10-13* **Shared designs aren't cleaned when opened.** Import .txt checks every piece (`designFromText`), but opening a design from Find designs, My designs or the stored copy (`load`) does not. Tested: an empty piece, x/y written as text, or a piece type named `__proto__` stop the page; a piece at x 500 is kept (marked "Off the map") instead of dropped. Fix: send every design through the same check as Import .txt. Same fix as the item above. (doc 06) *Done: `cleanDesign` runs in `load()` and Import .txt; drops bad pieces (null, text x/y, `__proto__`, off the map) and says how many; staging v155.*
- [x] *QA 10-13* **Haul it, Cash box says "Supplies (8 pallets)"** but counts every pallet and stack: Supplies, Ammo, Fuel and Mechanical (test base: 3 + 2 + 2 + 1 pallets + 12 fuel stacks = $3,320). Call it "Pallets and stacks", or one line per type. (doc 05) *Done: one line per type + a Crates line; team rows say "Pallets and stacks"; staging v155.*
- [x] *QA 10-13* **Clear can lose a design.** Clear empties the map at once, no question. Undo brings it back, but the stored copy is already empty, so a reload after a mistaken Clear loses the design (Undo lives only until reload). Ask first, or keep the last design until something new is placed. *Done: the stored copy is kept until something new is placed (no question; message after Clear); staging v155.*

## Polish
Things that work but could be better: looks, ease of use, small annoyances.

- [ ] **Random content without repeats**: pick content (jokes, events, tips) at random, but never show the same one twice in the same browser. Remember what's been shown on the device.
- [ ] **Look over the design view**: it has a lot of glitches. Example: the recon has no windows on its sides now. *QA 10-13: on the map the Recon Tower shows its windows as small white notches on N, W and E (2 each). Which view were they missing in: Side view, the Structure designer's 3D, or the map? Send a screenshot.*
- [ ] **Doors in the design**: they look ugly and don't show the door well.
- [x] *Claude QA* **Modify structure, wrong block for an entrance**: today it refuses and says which block to pick (Bunker: HESCO Small; Recon, Shelter: HESCO Large or Door). Try it; if it feels fussy, let it pick the right block for you instead. *Done: it now picks the right block and says so.*
- [ ] *Claude QA* **Gap rule**: the 1-square gap round emplacements is switched off and its checkbox hidden. Decide: bring it back, or delete it.
- [x] *Claude QA* **"Layer" means two things**: in Modify structure it's a floor of the structure; in Build it's how many pieces stand underneath. Rename one of them (e.g. "Floor" in Modify, which fits your Ground / Floor 2 / Roof idea above). *Done: Modify shows Ground · Floor 2 · Roof.*
- [x] *Claude QA* **Protection pictures ignore Modify changes**: an emplacement's hover picture still uses the structure as built. *Already fixed on test: added and removed blocks change the cover (checked: 3 HESCO on a Shelter roof take a Mortar from 590 m to 515 m). Left: a hole blown under a roof still counts as cover up to the roof.*
- [ ] *QA 10-13* **Empty map looks like an alarm.** A new map (FOB only) shows three red GETS IN and "with C4: 0". True, but it's the first thing a new player sees. Show "No walls yet" (grey) until something is placed.
- [x] *QA 10-13* **Build time "—" with only the FOB.** Deploying the FOB takes 4 s; show 0:04 (or "FOB only") instead of a dash. *Done: shows 0:04, "FOB deploy"; staging v155.*
- [ ] *QA 10-13* **"with C4" when they walk in anyway.** On a H1 wall the row says On foot GETS IN and with C4 **4**. Details explains it ("assuming the walls climbed over are made unclimbable first"), but the summary doesn't. Show "not needed" (grey), or add a small "if you raise the walls" under the number.
- [x] *QA 10-13* **Esc leaves Side view half on.** Press S, then Esc: the panel closes but the tool stays Side view, so clicking the map does nothing. Esc should go back to the piece you were using (like E). *Done: staging v155.*
- [ ] *QA 10-13* **Modify structure: the collapse warning covers the structure.** The "This destroys more than the block" box sits over the top of the map, on the Bunker you're working on. Put it in the Modify bar, or under the structure.
- [x] *QA 10-13* **Structure designer: test hint stays.** After Test collapse is switched off, its hint ("Click a block on this layer to remove it…") stays under the map, also after Save. *Done: cleared when the test ends; staging v155.*
- [ ] *QA 10-13* **Side view: mortar range labels pile up.** The "700 m" labels on each side of a Mortar overlap each other and are drawn through a Recon Tower standing next to it. Hide labels behind structures, or show them only for the hovered emplacement.
- [ ] *QA 10-13* **Ladder foot not shown on the map.** The square in front of a ladder must stay free (nothing can be built there), but the map draws the ladder inside the tower and the free square looks like any other. Mark it (hatched, "keep free").
- [ ] *QA 10-13* **Phones.** At phone width (390 px) the page is ~740 px wide and scrolls sideways; the step bar is cut off ("2 · HAU…"). Designing on a phone isn't needed, but Haul it (trips, Pack list) and Build order are handy on a phone next to the game. Make those two fit.
- [ ] *QA 10-13* **Pale grey text.** Accessibility check (axe): the small grey text under the steps and the notes on the Fact sheet are a bit too pale (contrast 4.1, needs 4.5). Darken `--muted`-style text slightly. Everything else passed. (doc 07)
- [ ] *QA 10-13* **Piece list cuts "Recon Tower"** to "Recon To…" below ~1100 px wide.
- [ ] *QA 10-13* **Fact sheet notes.** (a) Window C4 (1) is a guess (doc 12: confidence 30) but has no ESTIMATE mark. (b) Vendor price per stack note says "Some guides say $10 per unit"; it's $10 per 50-pack (facts review 12 Oct). (c) Trimmed Shelter / Trimmed Recon Tower still have their own rows in Build supplies and Hammer tier, though they left the piece list (only old designs use them).

## Add
- [ ] **bumber block** Let me do the 33% etc trick. Let me add bumber to a section if i forgot it. Make it work with brush *QA 10-13: partly there on test: Select → Add elevation adds Bumper blocks to a section, and Brush raises pieces next to a raised one when Auto elevation is on. What's the "33 % trick"? One line on how it works in game and this can be planned.*
- [ ] *QA 10-13* **Season 02 (15 Oct): new pieces and vehicles.** *Pieces on staging v156 (14 Oct) with guessed numbers; left: check them in game (below), MG Nest protection picture, vehicles.* MG Nest, Large Shelter and Wooden Step as pieces (the Large Shelter likely as a built-in structure from the Structure designer); Wolf-110, Wolf-110 Assault, T-72 and Gepard in the threat check if they change how high attackers reach, and in Haul it if they carry supplies. Needs the game checks under "Season 02" below first.
- [ ] *QA 10-13* **Redo** (Ctrl+Y / Ctrl+Shift+Z). Undo exists, Redo doesn't.
- [ ] *QA 10-13* **Ctrl+A selects everything** (in Select). Arrow keys already move a selection.
- [ ] *QA 10-13* **What changed in the threat check.** After an edit, say what got better or worse for a few seconds: "With a car: GETS IN → HOLDS".
- [ ] *QA 10-13* **Fix-it hints.** When a row says GETS IN, point at the cheapest fix: "Raise these 3 squares to H4 to stop the Ural". The threat check already knows the spots (weak points); this turns them into advice.
- [ ] *QA 10-13* **Builders > 1 split the build order**: who builds what, so two or three players can each follow their own list. Today more builders only shorten the total time.
- [ ] *QA 10-13* **Picture of the base for Discord**: one button that saves the map (or the Side view) as an image.
- [ ] *QA 10-13* **Version on the page.** Show the release date (e.g. "Test · 12 Oct c") in a corner, so testers can say which version they saw.
- [ ] *QA 10-13* **"Something broke" box.** When the page hits an error, show a small box with "Copy details" (error + design as text) for the feedback board, instead of failing quietly.
- [ ] *QA 10-13* **What's new on test.** A short list on `test.html` of what to try (from `PENDING_RELEASE.md`), so testers know where to look.


### Designs and templates
- [ ] **Find template page**: a page for browsing templates. *QA 10-13: done as Find designs (released 11 Oct b). Delete.*
- [ ] **My favourites**: mark designs you like. *QA 10-13: done, ★ in Find designs (11 Oct b). Delete.*
- [ ] **Design management**: search designs by tags, and by the design summary (build time, number of Urals needed, type of emplacements, protection level, etc.). *QA 10-13: done except tags (Find designs filters). Keep only "tags", or delete.*
- [ ] **Direct link to a design**: open a base design straight from a link with its ID, like `#132949324`. *QA 10-13: done, Copy link in Find designs (11 Oct b). Delete.*
- [ ] **Cap the number of saved designs**. *QA 10-13: done, 10 per player (11 Oct b). Delete.*
- [ ] **No-door warning in Build**: if the base has no doors, say "Hey, there's no way in, don't forget to get inside when you close this tomb".

### Build add-ons
- [ ] **Special tricks**.
- [ ] **Drop-down on buildables**: pick variants like Trim, half HESCO, etc.
- [x] **Straight line / free paint toggle**: easier building. *Claude QA*: already there, the "Straight lines" tickbox in the toolbar. Delete this if it's what you meant.
- [ ] **Auto-turn Bremers** when the line changes direction.

### Behind the scenes
- [ ] **Find designs: full card reload once a month** instead of once a week. Today each player reloads every card weekly (about 500 reads per player per week with 500 shared designs). Monthly cuts that to a quarter; the catch is that a deleted design can linger on a device a bit longer.
- [ ] *Claude QA* **One record per structure**: old Trimmed Recon / Shelter pieces and entrance seals are stored apart from Modify changes. Load them all as "structure + changes", so every tool reads one thing. Do this before more buildings arrive. (doc 11 §8)
- [ ] *Claude QA* **Keys in one place**: R and E are handled in three places (map, Modify structure, Structure designer), which is how they drifted apart. Gather them. *QA 10-13: there are 8 separate key listeners in the page today.*
- [ ] *QA 10-13* **Threat check slows down big bases.** It runs in full after every click and holds the page while it works: ~0.3 s per click on a 525-piece base (≈0.07 s on 70 pieces). Drag-painting a row is fine (one check per stroke). Fix: run it a moment after the last click, or in the background (a Web Worker), and grey out the old answer meanwhile.
- [ ] *QA 10-13* **Fonts are half the download.** The 11 embedded fonts are 274 KB in the page, 206 KB of the 436 KB players download (zipped). They never change, but every release downloads them again. Put them in a `fonts/` folder next to the page so browsers keep them between releases, and drop weights the page doesn't use.
- [ ] *QA 10-13* **Remove dead code** (found with a code checker, nothing calls it): `cycleSeal`, `nextSealText`, `laddersOf`, `dgfSideKey` + `DGF_SIDE`, `fndDepth`, `fndRoot`, `setVis`, `PHASES`, `selMsg`, `SV_BREM` / `SV_BREME`, the body of the attack's `follow()` (stops at `return`), an `if(false){…}` block in the map drawing, and about 25 unused values inside functions. Small, safe, makes the file easier to read.
- [ ] *QA 10-13* **Rename `history` and `status`.** The undo list is called `history`, which hides the browser's own `history` (the back button and page links). That blocks using links like `#design-id` with the back button later. Same for the `status()` function. Rename them (e.g. `undoStack`, `saveStatus`).
- [ ] *QA 10-13* **Reference designs as a test file.** Doc 12 §6 plans 5–8 known bases. QA used five (H2, double H2, H4 ring, Bunker inside H4, a full base); keep them in the repo (`tests/`) with a small script, and run it on every "Put it on test": page errors, threat rows, build time, Haul trips. Add the step to doc 08.
- [ ] *QA 10-13* **Keep the full Firebase rules in the repo** (`firestore.rules`). The docs hold only parts (cards, structures); the rules for `designs`, `users`, `facts`, `testers` and feedback live only in the console. One file = one place to check before a release, and a backup.
- [ ] *QA 10-13* **Card rules still allow "template".** `cards` read rule lets logged-out players read `visibility == 'template'` cards, but templates are gone and logged-out Find designs asks to log in. Drop that part next time the rules change. (doc 06)
- [ ] *QA 10-13* **Lock the Firebase key to the site.** In Google Cloud → Credentials, allow the web key only from `snurras.github.io`, and think about Firebase App Check. The key is public by design (it's in the page), so this stops other sites and scripts from using your Firebase quota.
- [ ] *QA 10-13* **`test.html` can show up in Google.** It has no "noindex" tag (`account-lab.html` has one). Add it to the test page so search results only show the live page.
- [ ] *QA 10-13* **Retire `account-lab.html`.** The login it was built for is live since 11 Oct. It's still online and talks to the live Firebase project. Delete it, or move it out of the published site.
- [ ] *QA 10-13* **A shared design can replace your own structure for the session.** Custom structures are named by id (`cs_…`). Opening someone's design that carries the same id swaps in their blueprint until reload. Rare; give each player's structures a per-owner prefix.

### Clean up: docs (*QA 10-13*)
Docs drift as the page grows. Each line is a small edit; "update the docs" in any chat with 01 can do them all.
- [ ] **01**: says "~6,000 lines, ~900 KB, nine modules". Today: ~7,000 lines, ~995 KB, ten modules (wd-find). Code map line numbers are from v138; all ten modules start 110–420 lines later now (e.g. `wd-app` 5317, `wd-find` 6704). The staging line is one long sentence of versions; keep only the current version there, history goes in the release notes.
- [ ] **00**: says the app is "~700 KB"; it's ~1 MB.
- [ ] **README.md**: two lines. Add what it is, the live and test links, and a list of the docs (00–12) with one line each, so a new chat or a friend finds their way.
- [ ] **Notes.md** is empty. Delete it.
- [ ] **Release notes**: 6 `RELEASE_*.md` files in the top folder, more each week. Move them to `releases/` (doc 08 points there).
- [ ] **06**: "Some comment tests (b46) are flaky" refers to a test nobody can find any more. Drop it, or name the test. Card rules comment still says "shared design / template".
- [ ] **11**: the header says v130 and "Still to do" lists things done since (3×3 blast and collapse in the threat check, v148). "Threat check on blocks (v123)" still says "collapse is not planned by the threat check". §8 points to "the assessment, I2", which doesn't exist. §9's "Code today (v105…)" line numbers are old. Suggest: one short "how it works now" part on top, history at the bottom.
- [ ] **11 §10 / 09**: the game questions are kept in two places (doc 11 §10 and "Check in the game" here). Keep them here only, and link from 11.
- [ ] **12**: still "Status: proposal". Fine, but the 12 Oct facts review (`FACTS_REVIEW_2026-10-12.md`) is the first run of it; link it from §0, and from 01's "Where things live".
- [ ] **10 (Base Defender)**: spelling (assesment, distrubuted, halfes, civs, lmg); the Sniper row has an extra column; the Scoreboards table is broken; "Clarify from original notes" has an open quote.
- [ ] **08**: add "run the reference designs" to "Put it on test" (see Behind the scenes).
- [ ] **This list (09)**: the empty `- [ ]` line under Add; "Launch ideas" has "Sign up with Gmail, or with email and password", which is live since 11 Oct.

### Check in the game
Answers fix guesses the planner makes today. Send as a short text list + 1–2 photos: "fact · planner says · you saw · Range or official".
**Where:** *Range* = Shooting Range is fine (shapes, heights, movement, what falls; the engine is the same everywhere). *Official* = do it on an official server, or in the Range only once the Range is calibrated (doc 12 §8): costs, build times, C4 and damage can be server settings.
Sorted: quick looks first, then the test session. Doc 12 has the confidence scale; doc 11 §10 has the structure questions.

**Quick looks (seconds each, any official server, no test needed)**
- [ ] *Official* **Build cost of a Bunker** in the build menu. Planner 61. If it's 61, all build costs are right (doc 12 review: game cost = datamine × 0.6 + 1). Note the number in the Range too: that is the first calibration point.
- [ ] *Official* **Unlock menu: Ural and Kodiak Driver level.** Planner 0 for both; guides say Ural Driver 3, Kodiak Driver 10. Easiest right after the Season 02 wipe (15 Oct), when nothing is unlocked.
- [ ] *Official* **Spawn screen: Kodiak and Humvee cost.** Planner $2,500 and $3,000; one guide says Kodiak $3,000.
- [ ] *Range* **Write down where these came from** (no source recorded, doc 12 review "?" list): jump and climb heights, stacking limits, FOB area 60 m, unloading times, vehicle trunks, Humvee bed, MH-6 level, Stingray angle.

**Calibrate the Range (once per season, ~15 min, doc 12 §8)**
- [ ] Same three measurements in the Range and on an official server: Bunker cost (build menu), time to build one HESCO Small with the Large Hammer, C4 to blow a Large HESCO. Same in both → the Range can be trusted for everything.

**Test session (Range is fine unless marked)**
- [ ] *Range* What can be added to a structure: HESCO inside the room, on the roof, on floor 2? What can the hammer take off? *How:* build each, try the hammer on each block, photo of what's left.
- [ ] *Range* Do pieces you built on a roof fall when the roof falls? (Planner: yes.) *How:* 2 HESCO on a Bunker roof, blow 2 corners, photo.
- [ ] *Official or calibrated* Windows: blow them with C4 (planner: 1), or do they only go when the roof falls? *How:* 1 C4 on a Bunker window, count charges until you can crawl in.
- [ ] *Official or calibrated* How many C4 does a Corner HESCO take? (Planner guesses 4, like a Large HESCO.) *How:* charges one at a time on a Bunker corner, count.
- [ ] *Range* C4 blast: does it reach blocks stacked on top (H2+)? (Planner: only blocks at the level of the one it was put on; what stood on them falls.) *How:* a 3-high column next to a 1-high one, 1 C4 at the base, photo. *1 C4 on sandbags takes the HESCO next to them: answered 12 Oct, in the planner.*
- [ ] *Range* Entrance opening height: H2 (planner's rule) or about 1.4 (Side view picture)? *How:* put a Small HESCO, then a Large, right outside a Recon entrance; can you still walk in?
- [ ] *Range* Does the floor raise the inside at all? Any windows or slits in the Shelter? *How:* stand inside next to a ground HESCO, photo from the side.

**Season 02 (from 15 Oct): new buildables** — for each of MG Nest, Large Shelter, Wooden Step (doc 11 §10 Q11):
- [ ] *Official* Build cost and hammer (build menu).
- [ ] *Range* Footprint in grids, height in HESCO units, which way it faces; 1–2 photos from above and the side.
- [ ] *Range* Can you stand on it, climb it, walk under it? Does it block a vehicle? Can it go on HESCO or next to a structure?
- [ ] *Official or calibrated* C4 to destroy; does it collapse in parts (like a structure) or all at once?
- [ ] *Range* MG Nest only: gun height and lowest angle, like the Mortar / CIWS tests (doc 04).

### Attack and other
- [ ] **Fields of fire on hover**: hovering over a firing port or window shows its shooting angles. (doc 04)
- [ ] **New piece – gate airlock**: a double gate entry (sluice) with firing ports. (doc 02)
- [ ] **New attack events**: scenario and joke outcomes for the attack animation. (doc 03)
  - **Murphy's Law**: everything that can go wrong does.
  - **Trojan Horse**: the enemy gets inside in disguise.
  - **Own goal**: the team opens the gate or door themselves.
  - **The Blob**: a mass arrives and every attack hits at once from several directions.
  - **Zombie apocalypse**: a cocky defender gloats: "They called me a crazy prepper, but look at me now – I'm ready for ya!" He throws the grenade but keeps the pin… or throws the pin and keeps the grenade (reference: The Thin Red Line).

## Dream big
Ideas for later.

- [ ] **Build with AI?** See if players can connect their own AI to the planner.
- [ ] **Patreon supporters as characters**: supporters show up as in-game characters.
- [ ] **Base Defender mini-game**: man your planned base with soldiers and defend it against attack waves. Everything about it, open questions included, is in [10_BASE_DEFENDER.md](10_BASE_DEFENDER.md).

### Launch ideas
- [ ] Max 500 users?
- [ ] Invite only?
- [ ] Moderators?
- [ ] Report button for comments?
- [ ] Replace like/dislike with less.
- [ ] Sign up with Gmail, or with email and password. *QA 10-13: live since 11 Oct. Delete.*
- [ ] Get more if your designs are well liked or used.
