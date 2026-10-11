# 09 · To-do list

What's next for the planner, sorted by kind of work. Tick an item (`[x]`) when it's done, then delete it after the next release.
The Base Defender mini-game has its own doc: [10_BASE_DEFENDER.md](10_BASE_DEFENDER.md).

## Fix
Things that are wrong or broken and hurt the player directly.

- [ ] **Modify Structure** Always show 3 Layers, Change to Ground, Rood, Floor 2. middle. To make it fast as middle is rarely used and Top, Bottom becomes most used for all.
- [ ] *Claude QA* **Threat check: C4 blast and collapse.** One C4 charge takes every block in the 3×3 squares around it (your game test), and blowing enough ground HESCO brings a roof down. The threat check uses neither yet, so C4 counts for thick walls are too high and bases look safer than they are. (doc 03, doc 11 §6)
- [ ] *Claude QA* **Side view: show Modify changes.** Blocks added with Modify structure and closed entrances aren't drawn in Side view yet (blocks taken off are). (doc 04)

## Polish
Things that work but could be better: looks, ease of use, small annoyances.

- [ ] **Random content without repeats**: pick content (jokes, events, tips) at random, but never show the same one twice in the same browser. Remember what's been shown on the device.
- [ ] **Look over the design view**: it has a lot of glitches. Example: the recon has no windows on its sides now.
- [ ] **Doors in the design**: they look ugly and don't show the door well.
- [ ] *Claude QA* **Modify structure, wrong block for an entrance**: today it refuses and says which block to pick (Bunker: HESCO Small; Recon, Shelter: HESCO Large or Door). Try it; if it feels fussy, let it pick the right block for you instead.
- [ ] *Claude QA* **Gap rule**: the 1-square gap round emplacements is switched off and its checkbox hidden. Decide: bring it back, or delete it.
- [ ] *Claude QA* **"Layer" means two things**: in Modify structure it's a floor of the structure; in Build it's how many pieces stand underneath. Rename one of them (e.g. "Floor" in Modify, which fits your Ground / Floor 2 / Roof idea above).
- [ ] *Claude QA* **Protection pictures ignore Modify changes**: an emplacement's hover picture still uses the structure as built.

## Add
New things for the planner.

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
- [ ] *Claude QA* **One record per structure**: old Trimmed Recon / Shelter pieces and entrance seals are stored apart from Modify changes. Load them all as "structure + changes", so every tool reads one thing. Do this before more buildings arrive. (doc 11 §8)
- [ ] *Claude QA* **Keys in one place**: R and E are handled in three places (map, Modify structure, Structure designer), which is how they drifted apart. Gather them.

### Check in the game
*Claude QA* Answers fix guesses the planner makes today. Send as a short text list + 1–2 photos (doc 11 §10).
- [ ] What can be added to a structure: HESCO inside the room, on the roof, on floor 2? What can the hammer take off?
- [ ] Do pieces you built on a roof fall when the roof falls? (The planner now says yes.)
- [ ] Windows: blow them with C4 (planner says 1), or do they only go when the roof falls?
- [ ] How many C4 does a Corner HESCO take? (Planner guesses 4, like a Large HESCO.)
- [ ] Entrance opening height: H2 (planner's rule) or about 1.4 (Side view picture)?
- [ ] Does the floor raise the inside at all? Any windows or slits in the Shelter?

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
