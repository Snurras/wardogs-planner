# 06 · Accounts, saving, Firebase & Fact sheet
Use for: logins, user settings, saved/shared designs, comments, the Fact sheet and anything that needs Firebase rules.

## Firebase (project `snurras-wardogs-base-planer`)
| Path | Holds | Notes |
|---|---|---|
| `designs/*` | saved designs (pieces + consumables plan) | personal, shared and template designs, comments, thumbs |
| `facts/main` | `{values, updated}` | edited Fact sheet values; **only the admin** can write |
| `users/{uid}` | `{levels, updated, tipsOff}` | saved with `setDoc(..., {merge:true})`; rule allows only these keys; `tipsOff` = list of ≤20 tip ids |
| `admins/*` | admin check | the admin UID lives only in the rules, never in the page |
| `testers/{uid}` | tester list (`{name}`) | added by hand in the Firebase console; a user can only read their own doc |
| `test_designs/*`, `test_feedback/*`, `test_facts/main` | test version data | only used by `test.html`; testers only |

## Test version (`test.html`)
- Same file as `index.html`. `TEST_MODE` is on when the page's file name is `test.html`; `FC(name)` maps `designs`/`feedback`/`facts` to `test_…`. `users/*` and `admins/*` are shared with live.
- Gate (`#testGate`, `testGate()`): covers the page until the user is logged in and `testers/{uid}` exists; shows the user id so a friend can send it. “TEST” badge in the top bar.
- Fact sheet in test: reads `test_facts/main`; until the admin saves one there, it shows the live `facts/main`.
- The code is public on GitHub; the gate hides the app, the rules protect the data.
- Without Firebase the page falls back to browser storage (`config/facts` etc.).
- Any change to stored fields needs a **rules change**: say so clearly in the release notes with the exact steps.

## Tips
Small bubbles pointing at easy-to-miss tools, one at a time, at most once per visit, right after the related action. “Never show this tip” → `tipsOff` (account when logged in, else browser). Tips: Entrances, Bremer face, Brush, Watch the attack, Build order, Pack list, Team. Code: `TIPS`, `showTip`, `tipAfterPlace`, `tipAfterStroke`.

## Fact sheet
- Every game number the planner uses, in groups (General; Ammo/fuel/mechanical; Build supplies; Build time; Hammer tier; C4; Heights; Direct ground fire protection; Movement; Stacking; Hammers; Unloading; Crates and pallets; Vehicles).
- Admin edits are saved for everyone; edited values are marked with “reset”. “Estimate” marks unmeasured numbers. Values are whole numbers within limits (`LIM`); new facts need a `LIM` rule.
- Read-only rules text below, written from the numbers; protection pictures section (doc 04).
- Copy sheet as text; Sources; disclaimer (fan project, not affiliated with BULKHEAD/Team17).

## Comments
Design comments + four feedback boards on About. Some comment tests (b46) are flaky.
