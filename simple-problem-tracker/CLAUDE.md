# Problem Tracker (simple-problem-tracker)

## Overview

A lightweight, single-page app for logging recurring problems. Each entry has a
title, an optional description, a **frequency** (daily / weekly / monthly / rarely),
a **severity** (low / medium / high / critical), a **status** (open / in progress /
solved; new entries start "open") and a capture timestamp. Entries are listed
newest-first. Status, severity and frequency can be changed later from the
dropdown "pills" on each card. A search box filters by title, and three color
swatches (blue = open, orange = in progress, green = solved) filter by status;
clicking the active swatch again shows all. Relative times ("5 min ago") refresh every minute.

## Tech Stack

- **HTML + CSS + vanilla JavaScript.** All of it is in `index.html`.
- **Persistence:** browser `localStorage` under the key `problemLog.simple.v1`
  (a JSON array of problem objects: `id`, `title`, `description`, `frequency`,
  `severity`, `status`, `createdAt` as an ISO string). `load()` migrates older
  entries without a `status` to `"open"`.
- **Browser APIs used:** `crypto.randomUUID` (falls back to `Date.now()`),
  `Intl.RelativeTimeFormat`, `toLocaleString`.
- **Running it:** open `index.html` directly in a browser. There is nothing to install.

## Development Notes

- No frameworks and no build step: everything stays in index.html.
- Never store data on a server; localStorage only.
- No external libraries or CDN links. Write everything in plain JavaScript, even small helpers.
- Render user-supplied text with `textContent`, never `innerHTML`, to avoid XSS.
- If the stored data shape changes, bump the storage key version (for example
  `problemLog.simple.v2`) or add a migration in `load()` so existing entries
  aren't lost.
