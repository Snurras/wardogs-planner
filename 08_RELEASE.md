# 08 · Test and release (when Snurra says “put it on test” or “release”)

## “Put it on test”
1. Run the tests on the staging copy; `pageerror` must be empty.
2. Publish the staging artifact (same URL).
3. Build the full page: `<!doctype html><html lang="en"><head>` + charset + viewport meta + the `<title>` and `<link rel="icon">` **taken out of the body** + `</head><body>` + the rest of the file + `</body></html>`. Open it once in a browser as `test.html` (served over http) and check the tester gate shows.
4. Save it as `test.html` in the repo and commit + push (`Put on test: <short summary>`). Keep `PENDING_RELEASE.md` up to date in the same commit.
5. If Firebase rules change, give Snurra the exact steps **before** testers try it.

## “Release”
1. Copy `test.html` to `index.html` **unchanged** (`cp`, don't open the file — no credits spent reading it).
2. Write `RELEASE_<yyyy-mm-dd>[b,c…].md` from `PENDING_RELEASE.md` (short bullets, plain language), then reset `PENDING_RELEASE.md`.
3. End the notes with **“Rules: no change needed.”** or the exact Firebase rules change with steps.
4. Commit + push `index.html`, the notes and `PENDING_RELEASE.md` (`Release <date>`).
5. Update the docs if anything in them changed (keep them short).

## No push access?
Send the files to Snurra instead; he uploads them to `Snurras/wardogs-planner` by hand.
