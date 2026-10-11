# Pending release (on staging / test, not released yet)

## Haul it, redesigned (staging v131–v138, on test 11 Oct 2026)
- The plan comes first: pick a vehicle at the top (each shows trips and total cash), then the trips in order with a picture of the bed, and a "Done" tick per trip.
- Free room on the last trip (a pallet spot or free crate stacks) is shown with one-tap buttons to fill it with Supplies, Ammo, Fuel or Mechanical.
- "Buy at spawn" list next to the trips. Stingray shots are not in it (paid at the emplacement), only in Cash.
- Pack list is a button in the top right of the plan: one block per player (team plans too), coloured chips, a Copy button each.
- New "Tune the load": one card each for Supplies, Ammo, Fuel and Mechanical with + / − buttons (see below). Shows minimal vs haul, spare as % (red under 10%, yellow under 25%, green), ammo shared evenly per emplacement, Drill Rig as % drill time, Stingray as shots + spare.
- Game colours: Supplies off-white, Ammo military green, Fuel rusty red, Mechanical dark grey.
- Settings moved to one box: levels, loading options, "Pallets Priority", "Use helicopters (Z20 Lakota, MH-6)", team ("One way" / "Round trips"), the design's parts and the per-emplacement plan (folded away).
- Repair reserve dropdown removed: spare Supplies do that job. Old drafts with a reserve keep it as extra Supplies.
- One cash total everywhere: the plan headline, the Cash box and the step bar now agree (FOB kit, hammer, supplies, vehicle).
- Stingray shots are not in the total: shown under it as "+ $5,000 / Stingray shot" (paid at the emplacement).
- One vehicle doing round trips is bought once, not once per trip.
- Haul priority in Settings: change the order the trips bring things in. Default Supplies, Ammo, Mechanical, Fuel. FOB kit and hammer always go first.
- Vehicle buttons show a pallet and/or crate symbol for how that vehicle packs it.
- No "Best" pick: vehicles always show in the same order (Ural, Kodiak, Z20 Lakota, MH-6, Humvee) with trips and cash, and you choose. The Ural (or the first one that can do it) is selected to start.
- Team plans follow Pallets Priority: drivers load pallets (plus trunk stacks), not crates.
- Free trunk slots are shown on each trip and in the free-room reminder, with a pointer to Tune the load.
- Wording: pallets "unload in one go".
- Tune the load: big buttons add or take one pallet (1,800), small dashed buttons one stack (50). Stacks fill up the pallet you already carry first ("planned" shows under the number). A Reset button takes all changes off.
- Ammo, Fuel and Mechanical show "Minimal" instead of "Need" and no spare bar (more is just more shots / drill time). Supplies keeps the spare bar.
- Team plans: + / − work again when the team is full; the card says how much won't fit.
- New pallet and crate symbols. Haul priority is a compact row under Team.
- Trunk packing: a small amount over a full pallet rides in the trunk (one slot per stack, FOB kit or hammer) instead of an extra pallet or trip. Example base: Ural 4 → 3 trips. Free trunk slots (on every trip) and free crate stacks fill in one tap. Helicopter trunks (Z20 Lakota, MH-6) hold countermeasures only, so they carry nothing for the base; the FOB kit and hammer go in the backpack.
- Fact sheet: new trunk sizes Kodiak 12 and Humvee 9 (one slot per item or stack), used by Haul it. Example base: Kodiak and Humvee 6 → 5 trips.
- Free-room texts: "Please think of the environment - One tap fills it all…" and "Thank you for thinking about the environment - Every spot on the bed is filled."
- Supplies, Ammo, Fuel and Mechanical icons look like the game's. "Minimal" on all four cards. Reset stands out (red) when there is something to reset.

## New login (staging v139, on test 11 Oct 2026)
- Log in with Google (one click), or with email and password.
- New email accounts get a "check your inbox" link; the account counts once it's clicked. Google accounts are checked already.
- "Forgot password?" emails a reset link (sent by Firebase). Nobody needs to ask the admin.
- First Google login asks for a planner name; the real Google name is never shown.
- Account button opens "Your account": name, email, Change name, Change password (email accounts), Log out.
- "Delete my account": removes the login, your saved designs and settings. Comments stay.
- Old name + password logins are retired: they see "Old login" and are asked to make a new account (fresh start). Their old designs stay on the old login.
- Bots: a hidden form field catches simple sign-up bots; email accounts must click the inbox link.
- Firebase console (before testers try it): Authentication → Sign-in method → enable Google; Settings → User actions → "Enable create (sign-up)" on; Authorized domains has snurras.github.io.
- Testers need a new `testers` document for their new user id (the gate shows it).

Rules: no change needed.
