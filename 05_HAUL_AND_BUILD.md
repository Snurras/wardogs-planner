# 05 · Haul, team & build order
Use for: supplies, vehicles, packing plans, team, pack list, cash, build times and build order.

## Haul it: how the page reads (redesign, staging v138)
Top to bottom, in the order a stressed player needs it:
1. **The plan** (green box): vehicle buttons in a fixed order **Ural, Kodiak, Z20 Lakota, MH-6, Humvee**, each with trips + cash and a pallet / crate symbol for how it packs. No "Best" pick: the player chooses (the Ural, or the first one that can do it, is selected to start). "Ways to pack it" when a vehicle has more than one. Headline: vehicle · trips, Total cash (+ $5,000 / Stingray shot under it), unload time, what it carries. Trip cards with a picture of the bed, trunk contents, free trunk slots and a "Done" tick. "Buy at spawn" list. **Pack list** button top right: one block per player (team too), coloured chips, Copy each.
2. **Free-room bar** (yellow): a free pallet spot (one tap = one pallet of the type you pick), or free crate stacks + free trunk slots on every trip (one tap fills them all). Texts: "Please think of the environment - One tap fills it all…" / "Thank you for thinking about the environment - Every spot on the bed is filled." Mentions fine-tuning in Tune the load.
3. **Tune the load**: one card each for Supplies, Ammo, Fuel, Mechanical. Big buttons ± one pallet (1,800), small dashed ±50 one stack (stacks change the planned amount, so they fill the pallet you already carry first; "planned" shows under the number after using them). **Reset** (red when active) takes all changes off. Cards show "Minimal" (the plan per emplacement). Supplies: spare bar + spare % (red < 10 %, yellow < 25 %, green). Ammo: shared evenly per emplacement. Fuel: Drill Rig as % drill time (100 % = one full run). Mechanical: Stingray shots + leftover spare. Team full → card says how much won't fit.
4. **Settings**: levels (saved to the user when logged in, else the browser), loading tickboxes (start supplies, FOB kit / hammer in backpack, **Pallets Priority**, **Use helicopters**), Team (rows **One way / Round trips**), **Haul priority** (compact row, default Supplies › Ammo › Mechanical › Fuel; FOB kit and hammer always first), the design's parts and "What Minimal is based on" (plan per emplacement), folded away.
5. **Cash**: one total, the same as the headline and the step bar. Vehicle bought once (round trips). Stingray shots are **not** in the total (paid at the emplacement): shown under it.

Colours follow the game: Supplies off-white, Ammo military green, Fuel rusty red, Mechanical dark grey (tokens `--build/--ammo/--fuel/--mech` + `-fill` / `-ink`, classes `.t-build` etc.). Icons as in game: framed grid, three rounds, fuel pump, gear.

## Packing (module `wd-haul`, `Haul.packFor(v,haul,levels,{palletPrio,first,prio,trunk,trunk1})`)
- Trip order from `plan.prio` (`Haul.rankOf`): each type's required part in that order, extra after all of them.
- **Trunk**: one slot per item or stack. Small top-ups ride in the trunk instead of an extra pallet / trip (example base: Ural 4 → 3 trips). Trip 1 trunk loses a slot per FOB kit / hammer kept there. Trunk sizes on the Fact sheet: Ural 6, Kodiak 12, Humvee 9. **Helicopters 0** (their trunk holds countermeasures only; forced in code).
- Pallets Priority: pallet vehicles use pallets; crates on one trip at most, and only when that saves a trip. Team plans pick the pallets-only load when it is on.
- Vehicles: Ural (2×8 bed, $5,000), Z20 Lakota (2×4, $7,400, Pilot lvl 10), Kodiak (1×4, one crate, $2,500), Humvee (1×4, $3,000, Driver lvl 15), MH-6 (2 racks of small crates, $6,250), on foot (15 stacks).
- Crates/pallets: pallet 2×4 cells, 1,800 supplies, $400; large crate 1×4 (35 slots, $300, Driver lvl 16); small crate 1×3 (24 slots, $150). Stack = 50 supplies, $10.
- Unloading at the FOB: pallets in one go (10 s); crates and trunk stacks by hand, 20 s full backpack run / 14 s one stack; 6 free slots.
- `plan.extra` may be negative (Tune the load takes some off). Old drafts' repair reserve % is turned into extra Supplies.
- Render code: `renderHaul()` in `wd-app` (prefix `hz-` for classes, `HZ_*` constants).

## Team
- Grid in Settings: rows One way / Round trips; columns Foot / Driver / Z20 Lakota / MH-6. Only ≥2 activates; red warning at 1. Code: `planTeam`, `teamOf`, `teamSize`, `TEAM_KINDS`. Each carrier buys its vehicle once.

## Build
- **Total time to build** (min:sec) with Builders dropdown 1–9, from in-game timing with a Large Hammer (one builder). Drill Rig time guessed from supplies. Trimmed buildings = full build + trim (Recon +30 s, Shelter +60 s). FOB deploy 4 s, remove 7 s; Guide blocks / top of Bumper block placed only (1 s, 1 supply); Bumper block's small HESCO is built and removed.
- Build order: edit by hand or let the planner suggest one; confirm to keep it; layers can be hidden. Bill of materials with trip tiles (icons: On foot, Ural, Z20 Lakota).
