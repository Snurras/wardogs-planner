# 09 · To-do list

What's next for the planner, sorted by kind of work. Tick an item (`[x]`) when it's done, then delete it after the next release.
The Base Defender mini-game has its own doc: [10_BASE_DEFENDER.md](10_BASE_DEFENDER.md).

## Fix
Things that are wrong or broken and hurt the player directly.

- [x] **Modify Structure** Always show 3 Layers, Change to Ground, Rood, Floor 2. middle. To make it fast as middle is rarely used and Top, Bottom becomes most used for all.
- [x] **Modify Structure** Shows you can get in 2h hesco in bunker/recon top floor. You cant. *Done: no HESCO Large or Door under a roof on corner HESCO (1.65 headroom).*
- [x] *Claude QA* **Threat check: C4 blast and collapse.** One C4 charge takes every block in the 3×3 squares around it (your game test), and blowing enough ground HESCO brings a roof down. The threat check uses neither yet, so C4 counts for thick walls are too high and bases look safer than they are. (doc 03, doc 11 §6)
- [x] *Claude QA* **Side view: show Modify changes.** Blocks added with Modify structure and closed entrances aren't drawn in Side view yet (blocks taken off are). (doc 04)

## Polish
Things that work but could be better: looks, ease of use, small annoyances.

- [ ] **Random content without repeats**: pick content (jokes, events, tips) at random, but never show the same one twice in the same browser. Remember what's been shown on the device.
- [ ] **Look over the design view**: it has a lot of glitches. Example: the recon has no windows on its sides now.
- [ ] **Doors in the design**: they look ugly and don't show the door well.
- [x] *Claude QA* **Modify structure, wrong block for an entrance**: today it refuses and says which block to pick (Bunker: HESCO Small; Recon, Shelter: HESCO Large or Door). Try it; if it feels fussy, let it pick the right block for you instead. *Done: it now picks the right block and says so.*
- [ ] *Claude QA* **Gap rule**: the 1-square gap round emplacements is switched off and its checkbox hidden. Decide: bring it back, or delete it.
- [x] *Claude QA* **"Layer" means two things**: in Modify structure it's a floor of the structure; in Build it's how many pieces stand underneath. Rename one of them (e.g. "Floor" in Modify, which fits your Ground / Floor 2 / Roof idea above). *Done: Modify shows Ground · Floor 2 · Roof.*
- [x] *Claude QA* **Protection pictures ignore Modify changes**: an emplacement's hover picture still uses the structure as built. *Already fixed on test: added and removed blocks change the cover (checked: 3 HESCO on a Shelter roof take a Mortar from 590 m to 515 m). Left: a hole blown under a roof still counts as cover up to the roof.*

## Add
- [ ] **bumber block** Let me do the 33% etc trick. Let me add bumber to a section if i forgot it. Make it work with brush
- [ ] 


### Designs and templates
- [ ] **Find template page**: a page for browsing templates.
- [ ] **My favourites**: mark designs you like.
- [ ] **Design management**: search designs by tags, and by the design summary (build time, number of Urals needed, type of emplacements, protection level, etc.).
- [ ] **Direct link to a design**: open a base design straight from a link with its ID, like `#132949324`.
- [ ] **Cap the number of saved designs**.
- [ ] **No-door warning in Build**: if the base has no doors, say "Hey, there's no way in, don't forget to get inside when you close this tomb".

### Build add-ons
- [ ] **Special tricks**.
- [ ] **Drop-down on buildables**: pick variants like Trim, half HESCO, etc.
- [x] **Straight line / free paint toggle**: easier building. *Claude QA*: already there, the "Straight lines" tickbox in the toolbar. Delete this if it's what you meant.
- [ ] **Auto-turn Bremers** when the line changes direction.

### Behind the scenes
- [ ] **Find designs: full card reload once a month** instead of once a week. Today each player reloads every card weekly (about 500 reads per player per week with 500 shared designs). Monthly cuts that to a quarter; the catch is that a deleted design can linger on a device a bit longer.
- [ ] *Claude QA* **One record per structure**: old Trimmed Recon / Shelter pieces and entrance seals are stored apart from Modify changes. Load them all as "structure + changes", so every tool reads one thing. Do this before more buildings arrive. (doc 11 §8)
- [ ] *Claude QA* **Keys in one place**: R and E are handled in three places (map, Modify structure, Structure designer), which is how they drifted apart. Gather them.

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
- [ ] Sign up with Gmail, or with email and password.
- [ ] Get more if your designs are well liked or used.
