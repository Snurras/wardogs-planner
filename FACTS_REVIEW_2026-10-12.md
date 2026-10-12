# Fact sheet review vs sources · 12 Oct 2026
First try of doc 12. Every number on the Fact sheet (`test.html` defaults, 193 facts) checked against the sources listed under Fact sheet → Sources, plus the official Steam patch notes since launch.
**Not included:** admin edits saved in Firebase (`facts/main`). Firebase can't be reached from Claude's sandbox. If you changed a value on the page, that row may differ.

## In short
- **No patch since launch changed a number the planner uses.** Patch 0.11, 0.1.2 and the October hotfixes only touch rewards, exploits, server browser and the CIWS vs Havoc time.
- **Build supplies: all 20 that the datamine lists fit one formula.** wardogs.tools shows the raw game values (Bunker 100, HESCO Small 15). The sheet's values (from AllThings.How and Skycoach) are exactly **raw × 0.6 + 1** for every one of them. Dakanoth's older figures (Bunker 81, Gate 69, Bremer 13, Mortar 121, Talon 801) are exactly **raw × 0.8 + 1**.
  So the game has a **build cost multiplier** (0.8 at some point before launch, 0.6 since Season 1). The sheet is right today. But one server setting can change every build cost at once, for example in Season 02 or on community servers.
- **Hammer tiers: 20 of 20 match** the datamine.
- **3 real mismatches**, all vehicles: Ural Driver level, Kodiak spawn cost, Kodiak Driver level.
- **Season 02 comes out 15 Oct 2026** (Steam news, 9 Oct preview). It adds new buildables (MG Nest, Large Shelter, Wooden Step) and new vehicles (Wolf-110, Wolf-110 Assault, T-72, Flakpanzer Gepard). That's the first real run of the patch routine.

| Suggested confidence | Facts |
|---|---|
| 100 Confirmed by tester | 66 |
| 90 Confirmed by user | 24 |
| 50 3rd party | 61 |
| 30 Best guess | 10 |
| ? no source recorded, you know | 24 |
| planner setting, not a game fact | 8 |

## Mismatches
| ID | Sheet | Sources say | What to do |
|---|---|---|---|
| `v.ural.lvl` | 0 ("no level needed", 4 Oct) | Driver 3 + $35k unlock (wardogshub, Dakanoth) | Look in the unlock menu once. Maybe it was unlocked on your account already, so you didn't see the level. |
| `v.kodiak.spawn` | $2,500 | $3,000 for "Kodiak [Pickup]" (wardogshub) | Look at the spawn screen. |
| `v.kodiak.lvl` | 0 | Driver 10 + $35k (was Driver 2) (wardogshub) | Look in the unlock menu. |

Small things, nothing to change in the numbers:
- `packPrice` note says "Some guides say $10 per unit". Dakanoth says $10 per **50-unit pack**, which is what the sheet uses. The note should say that.
- `mortar.ammo` 75 (your test) vs Dakanoth "about 20 per round, provisional". Your test wins.
- `v.mh6.racks` 2 (your test) vs Dakanoth "24 crate slots" (= one small crate). Your test wins.
- AllThings.How still has the pre-Season 1 FOB ($2,500) and Large Hammer ($1,600, level 7). It's out of date for those; the sheet has the new values.

## Missing from the sheet (found in sources)
- **Health per buildable** (wardogs.tools): Bunker/Recon/Shelter 5,000, Gate 5,320, Bremer 6,500, HESCO Large 2,250, Small 1,600, Door 2,200, Sandbags 735, FOB 15,000. Not needed today, but handy for C4 maths later.
- **FOB C4**: 5 C4 or 1 IED (Dakanoth). Only matters if the threat check ever targets the FOB itself.
- **Whole structure C4**: Bunker / Shelter / Recon 14 C4 (Dakanoth, citing a wardogs.zone table). The planner blows structures block by block from your tests, so this is not comparable 1:1.
- **Raw cost + multiplier.** Store the datamined cost and one multiplier (0.6) instead of one number per piece. After a patch, one look at one build cost in game then confirms them all. **Code**, small.

## Cheap checks (no test session needed, just a look)
1. **Build menu cost of a Bunker** (61?) → confirms the 0.6 multiplier, and with it every build cost. Do it again after Season 02.
2. **Unlock menu: Ural and Kodiak levels.** Spawn screen: **Kodiak cost.**
3. **Humvee spawn cost and level** (no source has it).

## The 24 "?" facts
Movement, climbing, stacking, FOB area, unloading, vehicle trunks, Humvee, MH-6 level, Stingray angle, `t.place`. No source and no note says where they came from. You probably measured most of them. Tell me which, and I'll set 100 or 90 with a date when the confidence code is built.

## Sources used (read 12 Oct 2026)
| Source | Date on page | Used for |
|---|---|---|
| [Steam news, WARDOGS](https://store.steampowered.com/news/app/1867240) (RSS feed) | patches 10 Sep – 9 Oct | what changed: nothing for the planner |
| [wardogs.tools buildables](https://wardogs.tools/database/buildables) | game version 499480 (site 2 Oct) | raw costs, hammer tiers, health, footprints |
| [Dakanoth](https://dakanoth.com/wardogs/) | prices re-checked 15 Sep | FOB, hammers, crates, packs, pallets, C4 |
| [wardogshub.gg logistics](https://wardogshub.gg/blog/wardogs-logistics-guide/) | 15 Sep | crates, pallets, vehicles |
| [AllThings.How building guide](https://allthings.how/wardogs-building-guide-how-to-set-up-a-fob-and-its-defenses/) | 11 Sep | build costs, hammer tiers |
| [Skycoach building guide](https://skycoach.gg/blog/wardogs/articles/building-guide) | 5 Sep | build costs |

Legend: ✓ sources agree · ✓* agrees through the 0.6 multiplier (raw wardogs.tools value shown) · ✗ differs · ≠ a source differs but your test wins · — no source covers it. Dates: the day the value was last confirmed at that level (source date, or your test date). Empty = not recorded.

## Every fact

### General
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `stack` | Supplies per stack / crate slot | 50 | ✓ | 50 | 2026-09-15 | Dakanoth: 50-unit packs |
| `packPrice` | Vendor price per stack ($) | 10 | ✓ | 50 | 2026-09-15 | Dakanoth: $10 per 50 pack. wardogshub says "$10 per unit" (likely wrong). Fix the planner note |
| `palletSize` | Supplies per pallet | 1800 | ✓ | 50 | 2026-09-15 | Dakanoth, wardogshub, AllThings: 1,800 |
| `palletPrice` | Pallet price ($) | 400 | ✓ | 50 | 2026-09-15 | Dakanoth, wardogshub: $400 |
| `fobPrice` | FOB kit price ($) | 7500 | ✓ | 50 | 2026-09-15 | Dakanoth: $7,500 (was $2,500; AllThings still says $2,500, older) |
| `fobStock` | Build supplies a new FOB lands with | 1400 | ✓ | 50 | 2026-09-15 | Dakanoth: 1,400 (1,200 before 18 Aug build) |
| `fobCap` | FOB cap per supply type | 20000 | ✓ | 50 | 2026-09-15 | Dakanoth, AllThings: 20,000 per type |
| `foot.stacks` | Supply stacks carried per trip on foot | 15 | ✓ | 50 | 2026-09-15 | Dakanoth: Operator/Assault pack 15 cells |

### Ammo, fuel and mechanical use
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `mortar.ammo` | Mortar · ammo supplies per shell | 75 | ≠ (yours wins) | 100 |  | Dakanoth says ~20 per round (provisional). Your test wins |
| `ciws.ammo` | CIWS · ammo supplies per reload | 250 | — | 100 |  | your test, no 3rd-party figure |
| `ciws.rounds` | CIWS · rounds per reload | 500 | — | 100 |  | your test, no 3rd-party figure |
| `talon.ammo` | Talon · ammo supplies per missile | 50 | — | 100 |  | your test, no 3rd-party figure |
| `sting.mech` | Stingray · mechanical per shot | 900 | ✓ | 100 |  | Also Dakanoth, AllThings: 900 |
| `sting.cash` | Stingray · cash per shot ($) | 5000 | ✓ | 100 |  | Also Dakanoth, AllThings: $5,000 |
| `drill.min` | Drill Rig · minimum fuel to run | 2400 | — | 100 |  | your test, no 3rd-party figure |
| `drill.max` | Drill Rig · fuel for full duration | 6000 | — | 100 |  | your test, no 3rd-party figure |

### Build supplies per piece
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `b.hesco_s` | HESCO Block (Small) | 10 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 10; wardogs.tools 15 (×0.6+1 = 10) |
| `b.hesco_l` | HESCO Block (Large) | 14 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 14; wardogs.tools 22 (×0.6+1 = 14) |
| `b.hesco_wall` | HESCO Wall | 46 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 46; wardogs.tools 75 (×0.6+1 = 46) |
| `b.bremer` | Bremer Wall | 10 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 10; wardogs.tools 15 (×0.6+1 = 10) |
| `b.door` | Door | 14 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 14; wardogs.tools 22 (×0.6+1 = 14) |
| `b.gate` | Gate | 52 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 52; wardogs.tools 85 (×0.6+1 = 52) |
| `b.bunker` | Bunker | 61 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 61; wardogs.tools 100 (×0.6+1 = 61) |
| `b.ifs` | Indirect Fire Shelter | 61 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 61; wardogs.tools 100 (×0.6+1 = 61) |
| `b.ifs_trim` | Trimmed Shelter | 61 | — | 30 |  | same as untrimmed (not in sources) |
| `b.recon_tower` | Recon Tower | 61 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 61; wardogs.tools 100 (×0.6+1 = 61) |
| `b.recon_trim` | Trimmed Recon Tower | 61 | — | 30 |  | same as untrimmed (not in sources) |
| `b.loudspeaker` | Loudspeaker | 61 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 61; wardogs.tools 100 (×0.6+1 = 61) |
| `b.radio` | Builder's Radio | 13 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 13; wardogs.tools 20 (×0.6+1 = 13) |
| `b.refuel` | Refuel Station | 121 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 121; wardogs.tools 200 (×0.6+1 = 121) |
| `b.repair` | Repair Station | 121 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 121; wardogs.tools 200 (×0.6+1 = 121) |
| `b.drill` | Drill Rig | 1351 | ✓ | 50 | 2026-09-11 | AllThings + Skycoach 1351 |
| `b.mortar` | L81 Mortar | 91 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 91; wardogs.tools 150 (×0.6+1 = 91) |
| `b.stingray` | Stingray | 91 | ✓ | 50 | 2026-09-11 | AllThings + Skycoach 91 |
| `b.talon` | Talon 9K-SAM | 601 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 601; wardogs.tools 1000 (×0.6+1 = 601) |
| `b.ciws` | Vanguard CIWS | 901 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 901; wardogs.tools 1500 (×0.6+1 = 901) |
| `b.sandbags` | Sandbags | 10 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 10; wardogs.tools 15 (×0.6+1 = 10) |
| `b.barbed` | Barbed Wire | 5 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 5; wardogs.tools 7 (×0.6+1 = 5) |
| `b.hedgehog` | Hedgehog | 14 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 14; wardogs.tools 22 (×0.6+1 = 14) |
| `b.recon_tent` | Recon Tent | 5 | ✓* | 50 | 2026-09-11 | AllThings + Skycoach 5; wardogs.tools 7 (×0.6+1 = 5) |

### Build time per piece (seconds, one builder, Large Hammer)
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `t.hesco_s` | HESCO Block (Small) | 3 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.hesco_l` | HESCO Block (Large) | 4 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.hesco_wall` | HESCO Wall | 7 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.bremer` | Bremer Wall | 3 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.door` | Door | 4 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.gate` | Gate | 8 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.bunker` | Bunker | 8 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.ifs` | Indirect Fire Shelter | 10 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.recon_tower` | Recon Tower | 8 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.loudspeaker` | Loudspeaker | 10 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.radio` | Builder's Radio | 4 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.refuel` | Refuel Station | 17 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.repair` | Repair Station | 17 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.drill` | Drill Rig | 186 | — | 30 |  | planner estimate |
| `t.mortar` | L81 Mortar | 11 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.stingray` | Stingray | 11 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.talon` | Talon 9K-SAM | 70 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.ciws` | Vanguard CIWS | 133 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.sandbags` | Sandbags | 3 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.barbed` | Barbed Wire | 2 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.hedgehog` | Hedgehog | 4 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.recon_tent` | Recon Tent | 2 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.trim.recon_tower` | Trim the Recon Tower (extra, after building it) | 30 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.trim.ifs` | Trim the Shelter (extra, after building it) | 60 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.fob` | Deploy the FOB kit | 4 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.remove` | Remove a built piece with the hammer | 7 | — | 100 | 2026-10-04 | your test, no 3rd-party figure |
| `t.place` | Place a block without hammering (Guide block, top of a Bumper block) | 1 | — | ? |  | no source recorded: you know where it came from |

### Hammer tier per piece (1 small · 2 medium · 3 large)
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `h.hesco_s` | HESCO Block (Small) | 1 | ✓ | 50 | 2026-10-02 | wardogs.tools: Small |
| `h.hesco_l` | HESCO Block (Large) | 2 | ✓ | 50 | 2026-10-02 | wardogs.tools: Medium |
| `h.hesco_wall` | HESCO Wall | 2 | ✓ | 50 | 2026-10-02 | wardogs.tools: Medium |
| `h.bremer` | Bremer Wall | 3 | ✓ | 50 | 2026-10-02 | wardogs.tools: Large |
| `h.door` | Door | 2 | ✓ | 50 | 2026-10-02 | wardogs.tools: Medium |
| `h.gate` | Gate | 2 | ✓ | 50 | 2026-10-02 | wardogs.tools: Medium |
| `h.bunker` | Bunker | 3 | ✓ | 50 | 2026-10-02 | wardogs.tools: Large |
| `h.ifs` | Indirect Fire Shelter | 3 | ✓ | 50 | 2026-10-02 | wardogs.tools: Large |
| `h.ifs_trim` | Trimmed Shelter | 3 | — | 30 |  | same as untrimmed |
| `h.recon_tower` | Recon Tower | 3 | ✓ | 50 | 2026-10-02 | wardogs.tools: Large |
| `h.recon_trim` | Trimmed Recon Tower | 3 | — | 30 |  | same as untrimmed |
| `h.loudspeaker` | Loudspeaker | 2 | ✓ | 50 | 2026-10-02 | wardogs.tools: Medium |
| `h.radio` | Builder's Radio | 1 | ✓ | 50 | 2026-10-02 | wardogs.tools: Small |
| `h.refuel` | Refuel Station | 3 | ✓ | 50 | 2026-10-02 | wardogs.tools: Large |
| `h.repair` | Repair Station | 3 | ✓ | 50 | 2026-10-02 | wardogs.tools: Large |
| `h.drill` | Drill Rig | 3 | ✓ | 50 | 2026-09-11 | AllThings: Large |
| `h.mortar` | L81 Mortar | 3 | ✓ | 50 | 2026-10-02 | wardogs.tools: Large |
| `h.stingray` | Stingray | 3 | ✓ | 50 | 2026-09-11 | AllThings: Large |
| `h.talon` | Talon 9K-SAM | 3 | ✓ | 50 | 2026-10-02 | wardogs.tools: Large |
| `h.ciws` | Vanguard CIWS | 3 | ✓ | 50 | 2026-10-02 | wardogs.tools: Large |
| `h.sandbags` | Sandbags | 1 | ✓ | 50 | 2026-10-02 | wardogs.tools: Small |
| `h.barbed` | Barbed Wire | 1 | ✓ | 50 | 2026-10-02 | wardogs.tools: Small |
| `h.hedgehog` | Hedgehog | 1 | ✓ | 50 | 2026-10-02 | wardogs.tools: Small |
| `h.recon_tent` | Recon Tent | 1 | ✓ | 50 | 2026-10-02 | wardogs.tools: Small |

### C4 to breach
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `c4.hesco_s` | HESCO Block (Small) | 4 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `c4.hesco_l` | HESCO Block (Large) | 4 | ✓ | 90 |  | Dakanoth: 0.21 charges/supply × 19 ≈ 4 |
| `c4.hesco_wall` | HESCO Wall | 4 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `c4.bremer` | Bremer Wall | 7 | ✓ | 90 |  | Dakanoth (wardogs.zone table 9 Sep): 7 |
| `c4.door` | Door | 1 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `c4.gate` | Gate | 2 | ✓ | 90 |  | Dakanoth (wardogs.zone table 9 Sep): 2 |
| `c4.sandbags` | Sandbags | 1 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `c4.window` | Bunker / Recon Tower window (blow a hole, then crawl in level with it) | 1 | — | 30 |  | open question (doc 11 Q5) |

### Heights (in HESCO units)
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `ht.hesco_s` | HESCO Block (Small) | 1 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.hesco_l` | HESCO Block (Large) | 2 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.hesco_wall` | HESCO Wall | 2 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.door` | Door | 2 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.gate` | Gate (barbed wire on top) | 3 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.bremer.face` | Bremer wall face | 3 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.bremer.footing` | Bremer footing | 1 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.bunker` | Bunker roof | 2 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.recon.edge` | Recon Tower roof, outer ring | 4 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.recon.centre` | Recon Tower roof, centre 2×2 | 5 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.ifs.edge` | Indirect Fire Shelter roof, outer ring | 2 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.ifs.centre` | Indirect Fire Shelter roof, centre 3×3 | 3 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |
| `ht.recon.window` | Recon Tower floor 2 (windows and ladder opening) | 2 | — | 90 |  | "your in-game tests" (Fact sheet → Sources), no date recorded. Add the date → 100 |

### Direct ground fire protection
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `dgf.ciws.pivot` | CIWS · pivot height above its floor (h) | 2 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.ciws.edge` | CIWS · pivot to the emplacement edge (grids) | 2 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.ciws.low` | CIWS · lowest angle (°) | -10 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.ciws.part` | CIWS · blocked up to this angle = some low angles blocked (°) | 0 | — | setting |  | planner setting, not a game fact: no confidence needed |
| `dgf.ciws.lim` | CIWS · blocked up to this angle = limited angles, steeper = poor (°) | 15 | — | setting |  | planner setting, not a game fact: no confidence needed |
| `dgf.ciws.reach` | CIWS · cover checked up to this many grids out | 8 | — | setting |  | planner setting, not a game fact: no confidence needed |
| `dgf.mortar.pivot` | L81 Mortar · pivot height above its floor (h) | 0 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.mortar.edge` | L81 Mortar · pivot to the emplacement edge (grids) | 1 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.mortar.low` | L81 Mortar · lowest angle (°) | 45 | — | 90 |  | fitted to your 5 Oct tests |
| `dgf.mortar.max` | L81 Mortar · max range (m) | 700 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.mortar.perDeg` | L81 Mortar · range lost per degree above the lowest angle (m) | 6 | — | 90 |  | fitted to your 5 Oct tests |
| `dgf.mortar.reach` | L81 Mortar · cover checked up to this many grids out | 5 | — | setting |  | planner setting, not a game fact: no confidence needed |
| `dgf.talon.pivot` | Talon · pivot height above its floor (h) | 1 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.talon.edge` | Talon · pivot to the emplacement edge (grids) | 1 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.talon.low` | Talon · lowest angle (°) | 0 | — | 90 |  | fitted to your 5 Oct tests |
| `dgf.talon.free` | Talon · blocked up to this angle still counts as all angles free (°) | 5 | — | setting |  | planner setting, not a game fact: no confidence needed |
| `dgf.talon.lim` | Talon · blocked up to this angle = limited angles, steeper = poor (°) | 20 | — | setting |  | planner setting, not a game fact: no confidence needed |
| `dgf.talon.reach` | Talon · cover checked up to this many grids out | 10 | — | setting |  | planner setting, not a game fact: no confidence needed |
| `dgf.sting.angle` | Stingray · drone launch angle, fixed (°) | 80 | — | ? |  | no source recorded: you know where it came from |
| `dgf.bremer.wall` | Bremer · wall thickness (% of a grid, on its face side) | 45 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.bremer.footLow` | Bremer · footing height at its tip (% of a HESCO height) | 30 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.bremer.footHigh` | Bremer · footing height where it meets the wall (% of a HESCO height) | 70 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.sb.h` | Sandbags · height (% of a HESCO height) | 65 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.sb.w` | Sandbags · width on top of a block (% of a grid, centred) | 20 | — | 100 | 2026-10-05 | your test, no 3rd-party figure |
| `dgf.minBlock` | Blocked bands smaller than this are ignored (°) | 3 | — | setting |  | planner setting, not a game fact: no confidence needed |

### Movement
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `move.step` | Step up without jumping | 1 | — | ? |  | no source recorded: you know where it came from |
| `move.jumpUp` | Jump over a 1-block gap: land this much higher at most | 1 | — | ? |  | no source recorded: you know where it came from |
| `move.longGap` | Long jump: gap you can clear landing no higher (blocks) | 2 | — | ? |  | no source recorded: you know where it came from |
| `climb.car` | Reach from a car roof (height) | 3 | — | ? |  | no source recorded: you know where it came from |
| `climb.ural` | Reach from a Ural Defender roof (height) | 4 | — | ? |  | no source recorded: you know where it came from |
| `climb.car.roof` | Car roof: stand height (crawl into a window level with it) | 2 | — | 30 |  | planner estimate |
| `climb.ural.roof` | Ural Defender roof: stand height (crawl into a window level with it) | 3 | — | 30 |  | planner estimate |

### Stacking limits
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `stack.hesco` | HESCO and doors stacked on HESCO / doors · max height | 7 | — | ? |  | no source recorded: you know where it came from |
| `stack.total` | Anything on top of a building · max height | 10 | — | ? |  | no source recorded: you know where it came from |
| `stack.bunker` | Bunker · highest base it can stand on | 2 | — | ? |  | no source recorded: you know where it came from |
| `rule.ladderStruct` | Structures may block a ladder (1 = yes, 0 = no). Game quirk, likely a bug: a structure can be placed so its own ladder, or the ladder of a structure already there, is blocked. Other pieces still can't go on the square in front of a ladder | 1 | — | 100 | 2026-10-12 | your test, no 3rd-party figure |
| `fob.area` | FOB build area (metres, square) | 60 | — | ? |  | no source recorded: you know where it came from |

### Hammers
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `ham.m.lvl` | Medium Hammer · Support level | 3 | ✓ | 50 | 2026-09-15 | Dakanoth: Support 3 |
| `ham.l.lvl` | Large Hammer · Support level | 8 | ✓ | 50 | 2026-09-15 | Dakanoth: Support 8 (was 7) |
| `ham.l.price` | Large Hammer price ($) | 2400 | ✓ | 50 | 2026-09-15 | Dakanoth: $2,400 (was $1,600; AllThings older) |
| `ham.l.unlock` | Large Hammer unlock fee ($) | 75000 | ✓ | 50 | 2026-09-15 | Dakanoth: $75k |

### Unloading at the FOB
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `unpack.pallet` | Drop a supply pallet and let it unload (s) | 10 | — | ? |  | no source recorded: you know where it came from |
| `unpack.runFull` | Crate → backpack → FOB and back, full backpack, 10 m run (s) | 20 | — | ? |  | no source recorded: you know where it came from |
| `unpack.run1` | The same with one stack (s) | 14 | — | ? |  | no source recorded: you know where it came from |
| `unpack.slots` | Free backpack slots when unloading crates (one stack each) | 6 | — | ? |  | no source recorded: you know where it came from |

### Crates and pallets
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `c.pallet.w` | Pallet · width (bed cells) | 2 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `c.pallet.l` | Pallet · length (bed cells) | 4 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `c.large.w` | Large crate · width (bed cells) | 1 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `c.large.l` | Large crate · length (bed cells) | 4 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `c.large.stacks` | Large crate · slots | 35 | ✓ | 100 | 2026-10-02 | Also wardogshub: 35 |
| `c.large.price` | Large crate price ($) | 300 | ✓ | 100 | 2026-10-02 | Also Dakanoth, wardogshub: $300 |
| `c.large.lvl` | Large crate · Driver level | 16 | ✓ | 50 | 2026-09-15 | Dakanoth, wardogshub: Driver 16 (was 20) |
| `c.small.w` | Small crate · width (bed cells) | 1 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `c.small.l` | Small crate · length (bed cells) | 3 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `c.small.stacks` | Small crate · slots | 24 | ✓ | 100 | 2026-10-02 | Also wardogshub: 24 |
| `c.small.price` | Small crate price ($) | 150 | ✓ | 100 | 2026-10-02 | Also Dakanoth, wardogshub: $150 |

### Vehicles
| ID | Fact | Sheet | Sources | Conf | Date | Source / note |
|---|---|---|---|---|---|---|
| `v.ural.w` | Ural · bed width (cells) | 2 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `v.ural.l` | Ural · bed length (cells) | 8 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `v.ural.trunk` | Ural · trunk items | 6 | — | ? |  | no source recorded: you know where it came from |
| `v.ural.spawn` | Ural · spawn cost ($) | 5000 | ✓ | 50 | 2026-09-15 | wardogshub: $5,000 |
| `v.ural.lvl` | Ural · Driver level | 0 | ✗ | 90 | 2026-10-04 | Sheet 0 ("no level needed", 4 Oct). wardogshub + Dakanoth: Driver 3 + $35k unlock. Check the unlock menu |
| `v.lakota.w` | Z20 Lakota · bed width (cells) | 2 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `v.lakota.l` | Z20 Lakota · bed length (cells) | 4 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `v.lakota.trunk` | Z20 Lakota · trunk items for the base (countermeasures only) | 0 | — | ? |  | no source recorded: you know where it came from |
| `v.lakota.spawn` | Z20 Lakota · spawn cost ($) | 7400 | ✓ | 50 | 2026-09-15 | wardogshub: $7,400 |
| `v.lakota.lvl` | Z20 Lakota · Pilot level | 10 | ✓ | 50 | 2026-09-15 | wardogshub: Pilot 10 |
| `v.kodiak.w` | Kodiak · bed width (cells) | 1 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `v.kodiak.l` | Kodiak · bed length (cells) | 4 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `v.kodiak.spawn` | Kodiak · spawn cost ($) | 2500 | ✗ | 30 |  | Sheet $2,500. wardogshub: "Kodiak [Pickup]" $3,000 |
| `v.kodiak.trunk` | Kodiak · trunk items | 12 | — | ? |  | no source recorded: you know where it came from |
| `v.kodiak.lvl` | Kodiak · Driver level | 0 | ✗ | 30 |  | Sheet 0. wardogshub: Driver 10 + $35k (was Driver 2) |
| `v.humvee.w` | Humvee · bed width (cells) | 1 | — | ? |  | no source recorded: you know where it came from |
| `v.humvee.l` | Humvee · bed length (cells) | 4 | — | ? |  | no source recorded: you know where it came from |
| `v.humvee.spawn` | Humvee · spawn cost ($) | 3000 | — | ? |  | no source recorded: you know where it came from |
| `v.humvee.trunk` | Humvee · trunk items | 9 | — | ? |  | no source recorded: you know where it came from |
| `v.humvee.lvl` | Humvee · Driver level | 15 | — | ? |  | no source recorded: you know where it came from |
| `v.mh6.racks` | MH-6 · crate racks | 2 | ≠ (yours wins) | 100 | 2026-10-02 | Dakanoth: 24 crate slots (= one small crate). Your test (2 racks) wins |
| `v.mh6.w` | MH-6 · rack width (cells) | 1 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `v.mh6.l` | MH-6 · rack length (cells) | 3 | — | 100 | 2026-10-02 | your test, no 3rd-party figure |
| `v.mh6.spawn` | MH-6 · spawn cost ($) | 6250 | ✓ | 50 | 2026-09-15 | wardogshub: $6,250 |
| `v.mh6.lvl` | MH-6 · Pilot level | 0 | — | ? |  | no source recorded: you know where it came from |