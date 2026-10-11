# 06 · Accounts, saving, Firebase & Fact sheet
Use for: logins, user settings, saved/shared designs, comments, the Fact sheet and anything that needs Firebase rules.

## Firebase (project `snurras-wardogs-base-planer`)
| Path | Holds | Notes |
|---|---|---|
| `designs/*` | saved designs (pieces + consumables plan) | personal and shared designs (old `template` ones count as shared: `visOf`), comments, thumbs; **My designs capped at 10** (page check, admin exempt) |
| `cards/*` | search card per shared design, same id as the design | Find designs; see below |
| `facts/main` | `{values, updated}` | edited Fact sheet values; **only the admin** can write |
| `users/{uid}` | `{levels, updated, tipsOff}` | saved with `setDoc(..., {merge:true})`; rule allows only these keys; `tipsOff` = list of ≤20 tip ids |
| `admins/*` | admin check | the admin UID lives only in the rules, never in the page |
| `testers/{uid}` | tester list (`{name}`) | added by hand in the Firebase console; a user can only read their own doc |
| `test_designs/*`, `test_feedback/*`, `test_facts/main`, `test_cards/*` | test version data | only used by `test.html`; testers only |

## Logins (released 11 Oct 2026)
- Google (popup) or email + password. Firebase keeps passwords and sends the verify / reset emails (Authentication → Templates; public name, sender name and support email set in the console).
- A login counts (`S.user`) only when complete (`acStep`): email checked (Google already is) and a planner name (`displayName`) picked. New Google accounts get `displayName` cleared so the real name never shows.
- Account dialog `#loginDlg` views: `acOut` · `acVerify` · `acName` · `acMe` (change name, change password, log out, Delete my account) · `acOld`. Code: `acStep`, `acShow`, `openLogin`, `authChanged`.
- Delete my account: re-login, then deletes own `designs` + `test_designs` (owner = uid), `users/{uid}`, then the login. Comments stay.
- Old name+password logins (`name@example.com`, `LOGIN_DOMAIN`) are retired: shown "Old login", counted as logged out.
- Hidden form field `lgWeb` catches simple sign-up bots. Later: 1-year clean-up of inactive accounts (not built).
- `account-lab.html`: the stand-alone test bench the login was built on.

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

## Design as text (10 Oct 2026)
- **Copy as text** (top bar) copies `designDoc()` as JSON. **Save .txt** / **Import .txt…** in the Open menu ("File on this device"): local file only, nothing is uploaded.
- Import: max 512 KB (`TXT_MAX`), must be a JSON object with `pieces`; `designFromText` keeps only known piece types on the map, cleans plan keys against `Haul.PLAN_DEFAULT`, names to plain text.
- Every blueprint that comes with a design (file, shared design, saved structure) goes through `cleanBlueprint` in `registerCustom`: known block types only, x/y 0–15, z 0–12, ≤ 2000 blocks, ≤ 40 structures, plain-text names.


## Find designs and cards (released 11 Oct 2026 b; templates removed in c)
- Module `wd-find` (end of the file), tab `find` in the **Tools** row. Hooks for the rest of the page: `window.FD` (`show`, `writeCard`, `tombstone`, `cardVis`, `openDesign`, `favEntries`, `onAuth`, `renameMine`, `dropMyStars`, `MAX_MINE`).
- **Card** `cards/{designId}`: `owner, ownerName, visibility, name, d` (JSON `{pieces,customs}` for the 3D preview), `s` (summary: `t` trips per vehicle with every vehicle unlocked, `sup`, `has` piece counts, `h` threat level 0 foot gets in · 1 car · 2 Ural · 3 holds, `c4`, `b` build seconds, `n`), `facts` (Fact sheet stamp → "Old numbers"), `fav` `{uid:true}` (★ count), `gone` (tombstone), `touched` (server time).
- **No templates** since 11 Oct 2026 c: only Personal and Shared. Written on Save when Shared; Personal again, Delete and Delete my account leave a tombstone (`gone:true`).
- **Device cache**: IndexedDB `wd_cards`; a visit asks only `touched > newest seen`; full reload weekly (monthly is on the to-do list). Logged out: Find designs asks to log in.
- Opening a result reads the full design once (`designs/{id}`) and adds it to `S.remote` (`addRemote`) so comments work. Live listeners left: my designs, the facts doc.
- 3D previews: `sv3dSvg` on the card's pieces via `withDesign` (swaps the design for a moment), drawn only when the card scrolls into view.
- Admin: **Make missing cards** (Find designs, bottom of the filters) makes cards for shared designs saved before cards existed and turns old templates into shared designs. 1 read + 1–2 writes each. Run once per data set (live / test).
- Published structures: kept on the device (`wd_pub_<collection>`), only `updated > newest seen` fetched; needs the composite index `visibility` + `updated` on `structures` and `test_structures` (built).
- Without Firebase (staging / browser) Find designs searches the designs kept here; cards are made on the fly.

### Card rules (in Firestore rules, inside `match /databases/{database}/documents`)
```
// Find designs: one search card per shared design / template (test version: test_cards)
function cardAdmin() { return exists(/databases/$(database)/documents/admins/$(request.auth.uid)); }
function cardTester() { return exists(/databases/$(database)/documents/testers/$(request.auth.uid)); }
function cardOk() {
  let n = request.resource.data;
  return n.keys().hasOnly(['owner','ownerName','visibility','name','d','s','facts','fav','gone','touched'])
    && n.touched == request.time
    && (!('d' in n) || n.d.size() < 700000);
}
function cardCreate() {
  let n = request.resource.data;
  return cardOk() && (n.owner == request.auth.uid || cardAdmin()) && n.get('fav', {}).size() == 0;
}
function cardUpdate() {
  let n = request.resource.data;
  let o = resource.data;
  return cardOk() && (
    // the maker (or the admin) updates the card; favourites stay as they are
    ((o.owner == request.auth.uid || cardAdmin()) && n.owner == o.owner && n.get('fav', {}) == o.get('fav', {}))
    // anyone logged in adds or removes only their own ★
    || (n.diff(o).affectedKeys().hasOnly(['fav','touched'])
        && n.get('fav', {}).diff(o.get('fav', {})).affectedKeys().hasOnly([request.auth.uid])
        && n.get('fav', {}).get(request.auth.uid, true) == true));
}
match /cards/{id} {
  allow read: if request.auth != null || resource.data.visibility == 'template';   // logged out: templates only
  allow create: if request.auth != null && cardCreate();
  allow update: if request.auth != null && cardUpdate();
  allow delete: if request.auth != null && (resource.data.owner == request.auth.uid || cardAdmin());
}
match /test_cards/{id} {
  allow read: if request.auth != null && cardTester();
  allow create: if request.auth != null && cardTester() && cardCreate();
  allow update: if request.auth != null && cardTester() && cardUpdate();
  allow delete: if request.auth != null && cardTester() && (resource.data.owner == request.auth.uid || cardAdmin());
}
```
