# 00 · Cheat sheet — which chat, which docs

## Why credits ran high
Every message in a long chat re-sends the whole history (hundreds of screenshots, code and test runs). The app file itself is also big (~700 KB). A short chat with only the right docs costs a fraction.

## The rule
**One topic per chat. Attach `01_PROJECT_CORE.md` + one topic doc. Start a new chat after each release or after ~20 messages.**

## Pick your chat
| I want to… | Attach | Model |
|---|---|---|
| Change a tool, piece, stacking rule, entrances, Wall Optimization, templates | 01 + 02 | Opus |
| Change how attackers get in, C4, movement, the attack animation or its jokes | 01 + 03 | Opus |
| Protection rules, hover picture, Side view, how pieces look from the side | 01 + 04 (+07 for look) | Opus |
| Haul, vehicles, packing, team, pack list, build times, build order | 01 + 05 | Opus |
| Logins, saving, comments, Fact sheet, Firebase rules | 01 + 06 | Opus |
| Colours, icons, layout, a new mockup | 01 + 07 + the feature doc | Opus |
| Fix a typo, change a number/fact, rename a label, quick question | 01 only | Sonnet (cheaper) |
| Release what's on staging | 01 + 08 | Sonnet |

## Starter prompt (copy, fill in)
```
Wardogs Base Planner. Read the attached docs first.
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
6. At the end of a chat, ask: **“Update the docs for what changed”** — attach the updated doc next time.
7. Measurements from the game: send them as a filled-in text list (like the questionnaire), plus 1–2 photos.

## Keep the docs in the repo
Upload the `docs/` folder to `Snurras/wardogs-planner` next to `index.html`. Then a new chat can also just be told: “Use the docs in the repo `Snurras/wardogs-planner`, folder docs.”

## Release (any chat with 08)
Say **“release”** → you get `index.html` + `RELEASE_<date>.md` → upload both to GitHub → do the Firebase rules step only if the notes say so.
