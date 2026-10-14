# Pending release (on staging / test, not released yet)

- **Add elevation** and **Remove elevation** in the selection bar. Select pieces, then raise them one level on a free foundation, or put raised pieces back on the ground. What stands on them moves with them.
- Add elevation uses as few Bumper blocks as possible: a group next to a raised piece needs none, and groups next to the same free square share one. The raised pieces are put in the build order as a chain, so the build order needs no extra Bumper blocks.
- In the build order, a Bumper block stays up while more pieces still need it, instead of a new one each time.
- **Brush**: with Auto elevation on, brushed pieces next to a raised piece are raised too, even if the brush had no elevation.
- **Elevation Stacking** is renamed **Auto elevation** (checkbox in the toolbar). The Fact sheet and tips say "elevation".
- **Threat check: C4 blast and collapse.** One charge now takes every block in the 3×3 squares around it (the charge sits in the square in front of the block it is put on), however few C4 it is: 1 C4 on Sandbags takes the HESCO next to them too. Blowing enough of a structure brings its roof down, by the same rules as Modify structure. The C4 list says what each charge takes and what falls.
- **Modify structure: floors.** The bar shows **Ground · Floor 2 · Roof** instead of Layer 1, 2, 3. Floor 2 is greyed out on a Bunker or Shelter.
- **Modify structure: headroom.** No HESCO Large or Door inside the Bunker or on Recon floor 2: the roof rests on 1.65-high corner HESCO.
- **Modify structure: entrances.** Recon and Shelter entrances take the block you pick (HESCO Small, HESCO Large, Door or Sandbags). The Bunker entrance only fits a HESCO Small, so it picks that for you and says so.
- **Modify structure: Doors and Sandbags** look right on the map (a Door symbol, a row of bags). **R** turns a new Door before you place it, or the Door you point at.
- **Modify structure: Sandbags in an entrance.** Take a block off next to an entrance to make it wider, then put Sandbags across it (they used to be refused or turned into a HESCO).
- **Modify structure: Floor 2 / Roof on the map.** With Floor 2 or Roof chosen, the map shows that floor over the structure: its blocks (e.g. the Shelter's centre 3×3), what was taken off, added or fell.
- **Modify structure: restore.** Erase (E) or right-click on a block you took off puts it back as built, any block, Corner HESCO (1.65) included. What fell with it comes back too.
- **Modify structure: new entrances.** A block taken off shows as a red square (no arrow); the red arrows stay on the original entrances. Any block can go in that square, and a Door there shows its preview and turns with R.
- **Modify structure: Doors on Floor 2 / Roof** show the Door symbol, not "D+".
- **Ladders and structures** (game quirk): a structure can be placed so it blocks its own ladder or another structure's ladder. Other pieces still can't go in front of a ladder. Fact sheet: *Structures may block a ladder* (set it to 0 if the game fixes it).
- **Modify structure: every floor on the map.** The chosen floor (Ground too) is drawn over the structure in the Structure designer's look: Sandbags as bags on the edge, Windows as a wooden frame on their sandbags, entrances marked ENTRY. Bunker and Recon floor 2 now look the same.
- **Block a window with Sandbags.** Pick Sandbags and click a window: they go on the sandbags under it and fill it, so no one crawls through (threat check too). Erase takes them off; erase again takes off the sandbags under the window; pick Sandbags and click to put them back. Works in the Structure designer too (Sandbags on the window's layer, H3 on the Recon).
- **Sandbags against a side.** Sandbags on the ground stand against one side of their two squares, as in the Structure designer (R turns them through all four sides): on the map, in Side view and in Modify structure. Sandbags on top of a block stay centred (that is what the protection test measured).
- **Labels H1, H2, HX** on HESCO Small, HESCO Large and the 1.65-high block, in Modify structure and in the Structure designer.
- **Corner HESCO is now called HESCO X Size** everywhere in the planner. In the Structure designer's 3D view it is 1.65 high and darker, with the 0.35 roof resting on it; the block list says H1.65.
- **Side view** (3D look) draws blocks added with Modify structure and closed entrances and centre squares.
- **Broken designs no longer break the page.** Every design is checked before it opens (the copy kept in the browser, Find designs, My designs, Favourites, Import .txt): broken pieces, pieces off the map and unknown piece types are left out, and the message says how many. If the copy kept in the browser can't be read at all, the map starts empty and says so.
- **Haul it, Cash box:** one line per type (Supplies, Ammo, Fuel, Mechanical: pallets + stacks), then the crates. Same total as before. In a team plan the line is called "Pallets and stacks".
- **Clear is safer:** after Clear, a reload still brings the old design back until you place something new. Undo works as before.
- **Esc leaves Side view** and goes back to the piece you were using (like E).
- **Build time with only the FOB** shows 0:04 (FOB deploy) instead of a dash.
- **Structure designer:** the Test collapse hint goes away when the test is switched off.
- **Season 02 pieces (first version, guesses until checked in game):**
  - **Large Shelter** (Structures): a thin 6×6 roof at H3 on 4 thin pillars, one in each corner square. The space under it is open: place pieces up to H3 under it (MG Nest, HESCO, a Bremer, …); anything taller is refused. Nothing can be built on a pillar's square (Fact sheet *rule.pillarFree*). The threat check lets attackers walk in under the roof; Side view draws the roof and pillars. Modify structure: take pillars off; 2 gone brings the roof down.
  - **MG Nest** (Emplacements): 1×1, H1. Can stand under the Large Shelter. Hover picture and Side view show a standing gunner on a tripod-mounted machine gun with its firing angles, graded like the Talon (gun height, edge and lowest angle are guesses on the Fact sheet).
  - **Wooden Step** (Walls & entry): open wooden stairs, 1×2, from H1 up to H2 (R turns it; the arrow points up). Side view draws real steps. You can walk up them or crawl under them (threat check too). Attackers can use them: stairs against an outside wall are a way in.
  - **Structure designer: Pillar** part (special): a thin post in one corner of a square (R picks the corner), holds a roof 3 layers up. The Large Shelter is in Examples. Your own structure on pillars with nothing on the ground works like the Large Shelter on the map.
  - Fact sheet: costs, build times, hammer, C4 and heights for the three, all marked ESTIMATE.

Rules: no change needed.
