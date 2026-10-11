# Pending release (on staging / test, not released yet)

- **Tools row** under Design it → Haul it → Build it: **Find designs** and **Structure designer** now live there, as tools that help the three steps. Fact sheet and About sit on the right of the top bar.
- **Open, name and Save together** on the right of the Tools row: **Open ▾** (Find designs…, ★ Favourites, Templates, My designs), the design name, Personal / Shared, **Save**, and **⋯** (Delete this design, Make template for the admin, Save as .txt file, Import .txt file…).
- **Find designs** (in Tools, also first in the Open menu): search every shared design and template.
  - Filters: name, maker or piece; Haul out (vehicle + max trips); Must have emplacements and stations (tap again = must not have); Protected against (on foot / car / Ural); least C4 to blow in; build time; templates / shared / favourites / mine; hide designs saved before the last Fact sheet change.
  - Results show the same 3D look as Side view, with a button to turn it. Sort by most ★, fewest trips, fastest build, hardest to get in, or newest. "Almost" shows designs that miss one filter, and says which.
  - Click a design for a big 3D view and its numbers; arrows step through the results. **Open in Design it** loads it, and **← Back to search results** returns with your filters kept (the browser Back button works too).
  - **Copy link** gives a direct link to a shared design (`#d/<id>`).
  - Your filters are remembered on this device. Logged out, Find designs shows the templates.
  - Trips assume every vehicle is unlocked (ⓘ explains it); Haul it uses your own levels.
- Saving as **Shared** now says it is in Find designs for everyone with a login.
- Changing your planner name updates it on your shared designs in Find designs. **Delete my account** also takes your ★ off other designs.
- The design title field no longer offers to fill in your name and address.
- Published structures are kept on the device too; a visit only fetches the ones that changed.
- **Favourites** (★): mark any shared design or template. The ★ count is how many players keep it, and it is what "Most ★" sorts by.
- **My designs: at most 10** saved online. Older accounts with more keep them, but can't add new ones until they delete some. A .txt file is the way to keep more.
- Less load on Firebase: the page no longer downloads every shared design on start-up. Each shared design has a small search card; the list is kept on the device and only changed cards are fetched.

Rules: **change needed** before testers try it. Firebase console → Firestore → Rules → paste this inside `match /databases/{database}/documents { … }` → Publish:

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

Index (one click): Firebase console → Firestore → Indexes → Composite → **Add index**: collection `structures`, fields `visibility` Ascending + `updated` Ascending, query scope Collection. Add the same for `test_structures`. Until it is built the page simply reads the whole list (nothing breaks).

After it is live: log in as admin → Find designs → **Make missing cards** (bottom of the filters) once, so designs shared before this update show up. Costs one read and one write per shared design and template.
