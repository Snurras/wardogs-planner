# 01 · Project core — attach to EVERY new chat

## What this is
**Wardogs Base Planner**: a web app for the game WARDOGS. Plan a base on the HESCO grid, check how attackers get in, work out what to haul, and get a build order.
- Owner: Snurra. Not a coder: everything is built by Claude. Talk in plain language, no code jargon.
- The whole app is **one HTML file** (~4,500 lines, ~700 KB): HTML + CSS + six `<script>` modules.

## Where things live
| What | Where |
|---|---|
| Staging (Claude's workbench) | claude.ai artifact https://claude.ai/artifact/BeyFVpAnFDRbygmRGARv9Z (version 105 at release 5 Oct 2026, evening) |
| Test version | `test.html` in the repo → https://snurras.github.io/wardogs-planner/test.html. Same code as `index.html`; the file name switches on test mode (tester login + `test_*` data, doc 06) |
| Production | GitHub Pages https://snurras.github.io/wardogs-planner/ (repo `Snurras/wardogs-planner`, file `index.html`) |
| Docs | the `0x_*.md` files in the repo root (these files) |
| Release notes | `RELEASE_<date>.md` in the repo; `PENDING_RELEASE.md` lists changes on staging that are not released yet |
| Firebase | project `snurras-wardogs-base-planer` (see doc 06) |

## How to start work in a new chat (for Claude)
1. Get the current code: read the staging artifact (Artifact tool, `read`), or clone the repo (`index.html` = last release, `test.html` = on test; staging may be newer).
2. Work on a local copy named `wardogs-base-designer.html` and **only open the parts you need** (use the code map below + grep). Don't read the whole file.
3. Test with Playwright (below), then publish to the **same staging artifact URL** (pass `url`).
4. Add a line to `PENDING_RELEASE.md` for every user-visible change, and say whether Firebase rules change.

## Workflow rules
- Changes go to **staging first**, then **test** when Snurra says “put it on test”, then production when he says **"release"** (doc 08).
- Big visual changes: **mockup first** (an image or a small review page), implement after "go".
- Snurra tests in the game and sends screenshots + measurements; trust those over assumptions.
- Never commit/push unless asked (“put it on test”, “release” and “update the docs” count as asking). The admin UID never goes in the page (only in Firebase rules). Don't send the email address anywhere.

## Code map (search for these headings; line numbers are approximate, v105)
| Module (`<script id=…>`) | Starts ~line | Contains |
|---|---|---|
| `wd-facts` | 711 | `WD` fact sheet: `WD.F(key)`, fact groups (`GROUPS`), limits (`LIM`), piece costs/heights/build times |
| `wd-design` | 939 | piece catalogue `P`, geometry, entrances, map drawing, protection maths + hover picture, Side view, select/brush, interaction, build order, templates |
| `wd-threat` | 2799 | threat check (movement graph, C4, routes), threat summary |
| `wd-attack` | 3223 | attack animation (soldier, vehicles, speech) |
| `wd-haul` | 3664 | supplies, packing (`Haul.packFor`), team, pack list |
| `wd-app` | 3827 | tabs, tips, fact sheet UI, saving designs, logins, comments, start-up |

Section headings inside `wd-design` (grep `/* ---------- `): geometry · entrances · symbols · drawing · height checks · **Direct ground fire protection** · **hover picture** · **Side view tool** · **3D pieces for the side view** · Fact sheet pictures · legend · select tool · brush · interaction · build order + BOM · templates.

Shared globals: `pieces` (the design), `P` (piece types), `mode`, `tool`, `C` (px per square), `M` (map margin), `N` (grid size), `$`, `el()`, `s()` (SVG element), `draw()`, `rectOf(p)`, `cellTop(p,x,y)`, `topOf(p)`, `R(p)` (rotation 0–3), `WD.F('key')`.

## Testing (Playwright, headless Chromium is installed)
```python
H=open('wardogs-base-designer.html').read()
pg.set_content('<!doctype html><html><head><meta charset=utf8></head><body>'+H+'</body></html>')
pg.evaluate("tipsOff=new Set(Object.keys(TIPS))")          # no tip bubbles in tests
pg.evaluate("load({v:2,pieces:[{t:'fob',x:40,y:40},{t:'mortar',x:21,y:21}]});$('zoomFit').click()")
```
Pieces: `{t:type,x,y,r(0-3),l:layer}`; stacked pieces get their height on load. Always check `pageerror` is empty.

## Writing style for Snurra
Short, plain sentences. Name things as the planner shows them (“Modify an entrance”, “Fact sheet”). Release notes as short bullet lists. One-line answers when possible.
