# 05 · Haul, team & build order
Use for: supplies, vehicles, packing plans, team grid, pack list, cash estimate, build times and build order.

## Supplies & haul (module `wd-haul`, `Haul.packFor(v,haul,levels,{palletPrio,first})`)
- Supplies box: build, “included now” row, ammo/fuel/mech, Drill fuel 1–5× full, **Pallets prio** tickbox. Extra/Total layout; “Total Supplies”.
- Trip priority: required build → ammo → first Drill fuel → mech → additional Drill fuel → extra build (`RANK`).
- Vehicles: Ural (2×8 bed, $5,000), Z20 Lakota (2×4, $7,400, Pilot lvl 10; name stays “Z20 Lakota”), Kodiak (1×4, one crate, $2,500), Humvee (1×4, $3,000, Driver lvl 15), MH-6 (2 racks of small crates, $6,250), on foot (15 stacks). Car icon exists for later.
- Crates/pallets: pallet 2×4 cells, 1,800 supplies, $400; large crate 1×4 (35 slots, $300, Driver lvl 16); small crate 1×3 (24 slots, $150). Stack = 50 supplies, $10.
- Unloading at the FOB: pallet 10 s; crates 20 s full backpack run / 14 s one stack; 6 free slots.
- Cash estimate follows the selected plan; “Select” button in All options.
- Pack list (collapsible, for Discord).

## Team
- Grid under the other options: rows One way / Transporters; columns Foot / Driver / Z20 Lakota / MH-6. Default 0; only ≥2 activates; red warning at 1; “No heli” option hidden when the team is used. Cash estimate per team member. Code: `planTeam`, `teamOf`, `teamSize`, `TEAM_KINDS`.

## Build
- **Total time to build** (min:sec) with Builders dropdown 1–9, from in-game timing with a Large Hammer (one builder). Drill Rig time guessed from supplies. Trimmed buildings = full build + trim (Recon +30 s, Shelter +60 s). FOB deploy 4 s, remove 7 s; Guide blocks / top of Bumper block placed only (1 s, 1 supply); Bumper block's small HESCO is built and removed.
- Build order: edit by hand or let the planner suggest one; confirm to keep it; layers can be hidden. Bill of materials with trip tiles (icons: On foot, Ural, Z20 Lakota).
