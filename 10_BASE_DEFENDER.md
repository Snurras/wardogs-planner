# 10 · Base Defender (mini-game)

A mini-game where you man your planned base with soldiers and defend it against attack waves. Later-stage work, almost a side project. Listed under Dream big in [09_TODO.md](09_TODO.md).

## 1. Core loop
- You staff the defences and move soldiers around during the attack.
- Levels are defined by number of defenders vs. number of attackers. Attackers always outnumber defenders.
- Each base gets two attacks, one from each colour/side. The setup can't be changed between them, but ammo is restored.
- Attacks come from a random direction, but the vehicles/unit types per level are fixed.
- 3 attempts per level; fail all three and you drop back to the first (see open questions).
- Higher levels unlock different weapons, meds, etc.

## 2. Economy
- The base budget is set by the level, measured in number of Ural trucks carrying pallets.

## 3. Damage, cover and armour

| Defender position | Damage taken |
|---|---|
| In the open | 100% |
| Half cover | 50% |
| Window or firing port | 10% |

- Armour works like a second health bar: 100 armour + 100 health = 200 damage absorbed. Damage is evenly distrubuted between armor and health. A soldier with  100 health and 100 armor, taking 20 damage will have 90 health and 90 armor.
- After being fully killed and then revived, a soldier comes back with 50% armour. Same logic applies to medic, if a soldier is down to 50% life, 25%of armored is consumed, healing restores life but not armor.
- Barbed wire can be destroyed by gunfire or explosives, it has 100 health.
- Fields of fire matter: placement of windows and ports decides who can shoot where.

## 4. Defender units – inside the base

| Unit | Role | Notes |
|---|---|---|
| Grunt | Cheap infantry | Can man positions and shoot |
| Base specialist | Can repair and are 10% more efficient in emplacements | Can man positions and with UZI, lacks range but efficient on short distance |
| Rifleman | Better infantry | Better aim, throws grenades; worse on emplacements |
| LMG | Suppression | Can only man windows/walls |
| Medic | Support | Gives meds and revives; only fires as base specialists |
| Sniper | Precision | Misses when enemy is: 75% vs. running targets, 25% vs. jumping, never vs. stationary | Deals 100 damage, can deal headshot with double kill. If hitting, 20% vs running, 25% vs jumping and 50% vs standing still. 
| Hawkeye | Sniper-scout near the base | Like recon, but only spots just before the attack; can also kill outside the base |

## 5. Defender units – outside the base
- **Single Recon**: spots enemies before the attack. More recon = higher chance. Helicopters are very easy to spot, ground units harder. Example: "Enemy attack bird incoming" 10 s before spawn; each extra recon adds +20%, up to 15 s warning.
- **Recon & demo**: can destroy vehicles before they arrive, but can be killed (like outer specialists).
- **Outer specialists** (supply-line disruption): hit artillery, Urals, Humvees etc. before they become visible. Their chance of being killed rises with every successful strike.

## 6. Defender vehicles (all improve with recon)

| Vehicle | Effective against |
|---|---|
| Humvee | Infantry, before they spawn |
| Havoc | Infantry, artillery, tanks |
| Tank | Other vehicles; small chance vs. helicopters |
| Gepard? | Undecided (likely anti-air) |

## 7. Defensive equipment
- **Mines**: placed against vehicles or infantry.
- **Grenade launchers**: found in crates.
- **Stingray** (anti-vehicle): Requires recon or that you take fire. Flow: recon reports "Tank spotted" → you man the Stingray → fire within 15 s of the tank entering and it dies; otherwise it survives an extra number of seconds. Same for Humvees. Rocket launchers also work.
- **Anti-helicopter**: 1 CIWS will win vs Heli, Talon 25% on first, 75% on second and 100% on third. Can shoot earlier with recon, green will light up 5s before Heli appears. 
- No own artillery exists.

## 8. Mortars
Enemy mortar accuracy ramp (per shot): 1st random within fob square, 2nd 25% chance to hit a the high-value target, then 50%, 75%, 100%. Shots always lands and can take out random soldiers within one grid and emplacements with direct hit. (civs take 3 hits center, outer counts as 0.5) Shoot prio: Mortar, CIWS, Stingray, Talon, gates, walls.

Own mortar:
- Uses the same ramp, but recon halfes the chance of miss.
- 2 mortars don't increase hit chance; they give more attempts.
- A firing mortar has x% chance to reduce attackers before they spawn. Low effect by design: mortars should only be manned during an attack.
- Balancing test for mortar duel: 1 vs 1 is 60/40 for enemy, with recon support its only 30/70.

## 9. Enemy threats
- **Infantry types**: Sniper, LMG, Demo max 4c4 can use rockets?, Assault max 2c4. Juggernaut (high armor, slow, lmg)
- **Helicopters**: also attack the base.
- **APC**: keeps spawning new troops until destroyed, both for attackers and defenders.
- **Tanks, Humvees, Urals**: countered as above.
- **Artillery**: only killable by recon + support, or Stingray with recon + support:
  - Killing artillery while under fire: 60 s.
  - If recon + support are already in the field: 20 s, plus 50% chance to kill it before it attacks.
  - With Stingray: 20 s to counter; 10% per recon to detect before the first shot.
  - With your own Havoc, 40s after first hit, 30 with recon.

## 10. Drill
- An expensive option that can win the match faster, e.g. skip the last 40% of the attack.
- Idea: it also makes the fight more intense (to be decided).

## 11. Scoreboards
Per level, plus total time across all bases.

| Category | Rules |
|---|---|
Full campaign
| Flawless | Fastest, no extra attempts, no deaths in the base |
| No surrender | Fastest, no extra attempts, deaths allowed |
| Any | Fastest, attempts not counted |
Single scenarios 
| Flawless Fastest, no deaths in the base |
| Fastest, deaths allowed |

## 12. Open questions
Design decisions still to make, plus notes that were ambiguous when translated.

### Design decisions
- [ ] How should build time affect the game?
- [ ] Size classes (small / medium / large) where build time is regulated – larger classes are more complex. Worth doing?
- [ ] Completing a level gives more resources – can players save them for later?
- [ ] Drill: does it only shorten the match, or also make the fight more intense?
- [ ] Gepard: include it, and with what role?
- [ ] Stingray: how many extra seconds does a vehicle survive if you fire too late?

### Clarify from original notes
- [ ] "3 attempts per level, otherwise back to the previously level.

