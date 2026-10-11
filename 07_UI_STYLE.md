# 07 · Look & feel
Use for: colours, fonts, icons, layout, mockups. Attach together with the feature doc it concerns.

- Military-olive theme, light and dark (tokens on `:root`, dark via `prefers-color-scheme` and `data-theme`). Key tokens: `--bg #E7EAE1`, `--panel #F4F6EF`, `--ink #1F251B`, `--muted #5B6452`, `--line #C9CFBE`, `--accent #4D5C27`, `--bad`, `--ok`, haul types `--build/--ammo/--fuel/--mech` (game colours: off-white, military green, rusty red, dark grey; each with `-fill` and `-ink`), `--sand`, `--concrete`, `--steel`, `--tent`, `--camo1/2`.
- Fonts: Saira Condensed (headings), Barlow (body), IBM Plex Mono (data), Saira Stencil One (title). All embedded.
- Toolbar icons: small coloured SVGs (pointer, eyedropper/brush, eraser, green exit sign, wand over wall, IED for Clear, eye-over-blocks for Side view).
- Favicon: the Large Hammer (version H2, gold rim, no background).
- Side-view art: flat icon style with 3D boxes, sand-coloured HESCO with wire grid and corner posts, beige Bremer concrete, olive soldier.
- Process for visual changes: Claude makes a mockup (image or a small private review page with zoom), Snurra comments, then it goes to staging. Ask for one batch of feedback per round.
- Haul it icons: Supplies framed grid, Ammo three rounds, Fuel pump, Mechanical gear (as in game); pallet = angled pallet with slats, crate = toolbox outline.
- Tools row: slim (28 px) boxy buttons with a bracket line and "TOOLS" label, one level below the arrow steps; menus are popovers (`.popm`, `.pmi`) in the panel colour.
