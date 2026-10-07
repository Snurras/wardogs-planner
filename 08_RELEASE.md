# 08 · Release checklist (when Snurra says “release”)
1. Run the tests on the staging copy; `pageerror` must be empty.
2. Publish the staging artifact (same URL).
3. Build `index.html`: `<!doctype html><html lang="en"><head>` + charset + viewport meta + the `<title>` and `<link rel="icon">` **taken out of the body** + `</head><body>` + the rest of the file + `</body></html>`. Open it once in a browser to check.
4. Write `RELEASE_<yyyy-mm-dd>[b,c…].md` from `PENDING_RELEASE.md` (short bullets, plain language), then reset `PENDING_RELEASE.md`.
5. End the notes with **“Rules: no change needed.”** or the exact Firebase rules change with steps.
6. Send `index.html` and the notes to Snurra; he uploads them to `Snurras/wardogs-planner` by hand.
7. Update the docs in `docs/` if anything in them changed (keep them short).
