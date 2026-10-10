# 00 · Cheat sheet — which chat, which docs

## Why credits ran high
Every message in a long chat re-sends the whole history (hundreds of screenshots, code and test runs). The app file itself is also big (~700 KB). A short chat with only the right docs costs a fraction.

## The rule
**One topic per chat. Point Claude at `01_PROJECT_CORE.md` + the topic doc(s) in the table below — usually one, structures need two or three (they live in the repo, no need to attach). Start a new chat after each release or after ~20 messages.**

## Pick your chat
| I want to… | Docs | Model |
|---|---|---|
| Change a tool, piece, stacking rule, entrances, Modify structure, Wall Optimization, templates | 01 + 02 (+11 for structures) | Opus |
| Change how attackers get in, C4, movement, the attack animation or its jokes | 01 + 03 | Opus |
| Structures as blocks, Structure Builder, modify a structure (Bunker, Recon, Shelter, new buildings) | 01 + 11 (+03 threat, +04 side view) | Opus |
| Protection rules, hover picture, Side view, how pieces look from the side | 01 + 04 (+07 for look) | Opus |
| Haul, vehicles, packing, team, pack list, build times, build order | 01 + 05 | Opus |
| Logins, saving, comments, Fact sheet, Firebase rules | 01 + 06 | Opus |
| Colours, icons, layout, a new mockup | 01 + 07 + the feature doc | Opus |
| Fix a typo, change a number/fact, rename a label, quick question | 01 only | Sonnet (cheaper) |
| Add to or sort the to-do list, Base Defender ideas | 01 + 09 (+10) | Sonnet |
| Put staging on the test version / release test to everyone | 01 + 08 | Sonnet |

## Starter prompt (copy, fill in)
```
Wardogs Base Planner. Repo Snurras/wardogs-planner — read 01_PROJECT_CORE.md and <topic doc> there first.
Staging: https://claude.ai/artifact/BeyFVpAnFDRbygmRGARv9Z (newest code — work from it, only open the parts you need).
Task: <what you want>.
Mockup first: <yes/no>.  Put it on staging when done: <yes/no>.
```

## Habits that save credits without slowing you down
1. **Batch feedback**: collect all comments on a mockup, send them in one message.
2. **Crop screenshots** to the part that matters; send fewer, smaller images.
3. Say **“mockup as one image”** for quick looks; ask for a review page only when you need to zoom.
4. Say **“no explanation needed, just do it”** for small changes.
5. When a chat goes off-topic, **start a new one** with the matching doc.
6. At the end of a chat, ask: **“Update the docs for what changed”** — Claude updates them in the repo.
7. Measurements from the game: send them as a filled-in text list (like the questionnaire), plus 1–2 photos.

## Three versions
| Version | Address | Who sees it |
|---|---|---|
| Staging | the claude.ai artifact | only you (Claude's workbench) |
| Test | https://snurras.github.io/wardogs-planner/test.html | logged-in testers only (Firebase list `testers`), own designs, feedback, facts and structures; logins and user settings are shared with Live |
| Live | https://snurras.github.io/wardogs-planner/ | everyone |

## The two commands (any chat with 08, Sonnet is fine)
- **“Put it on test”** → Claude builds the page from staging and puts it in the repo as `test.html`. You and your friends try it.
- **“Release”** → Claude copies `test.html` to `index.html` unchanged, writes `RELEASE_<date>.md`, puts both in the repo. Do the Firebase rules step only if the notes say so.
- Claude commits to GitHub itself when it has push access; otherwise it sends you the files to upload.

## Add a tester
1. The friend opens `test.html` and logs in; the page shows their user id.
2. Firebase console → Firestore → `testers` → Add document → Document ID = that user id → add one field `name` (string) = their name → Save. Done, they're in on next reload.
3. To remove someone: delete their document.
Your own account needs a `testers` document too.
