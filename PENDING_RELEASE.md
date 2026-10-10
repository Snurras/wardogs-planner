# Pending release (on staging / test, not released yet)

- Threat check: two Bremers back to back (faces on the same line) now count as the higher wall. A raised Bremer with a plain one behind it no longer lets a car in.
- Threat check: no more climbing onto a neighbouring Bremer top straight through a higher wall face.
- Threat check (C4): blowing one of two back-to-back Bremers no longer opens the line; the other face still blocks.
- Threat check: a Bremer right outside an entrance or window, with its face toward the building, now covers that opening. Attackers can still walk on its footing, but not through the wall into the building. Shown in the Fact sheet rules.
- Threat check: no more dropping into an entrance from on top of a block right outside it. An entrance is as tall as a Door; anything outside that reaches its top closes it. Shown in the Fact sheet rules.
- Threat check: a Bremer at the foot of a Recon Tower ladder, face toward the tower, now blocks the ladder.

- New: **Structure designer** (link under the piece list, above Legend). Build a structure block by block, layer by layer, on its own 10×10 area: HESCO, sandbags, door, plus floor, roof, window and ladder. Properties (cost, build and trim time, seal, collapse rule), a 3D view, a C4 / collapse test, and examples of the Recon Tower, Shelter and Bunker. Save your own under My structures; the admin can publish them. Not used on the base map yet.
- New: **place your own structures on the map**. Under the Structure designer link, pick one of your saved or published structures and click its icon, then click the map, like any other building. Entrances, windows, ladder, height, cost and build time come from the structure. Saved designs keep the structures they use, so they open for everyone. Side view shows them as plain HESCO blocks for now.
- Structure designer 3D view: ▲ ▼ arrows at the layer corner move the layer up and down (the map follows), N / E / S / W on the sides, "Hide above layer" (was "Cut above layer"). **Maximize** (bottom right) swaps the 3D view and the layer map; **Windowed** swaps them back.

Rules: **change needed** for the Structure designer: new collections `structures` and `test_structures` (rules in doc 11, section 11). Until then saving structures online is refused; the rest works.
