# 🏓 Pickleball 2026 Tournament — Harisumiran Columbus

A single-file web app for running a 24-team doubles pickleball tournament: match schedule across 4 courts, a referee scoring console, live standings, qualification tracking, and a knockout bracket. Everything is in **`index.html`** — no build step, no server required.

**Live site:** _add your GitHub Pages / Firebase Hosting link here once published_

---

## Features

- **📅 Match Schedule** — 6 groups of 4 played as round robin on 4 courts in 9 timed waves (starts 4:00 PM, ~20 min each). Groups A/C/E play on Courts 1 & 2; B/D/F on Courts 3 & 4, so every team stays on its designated courts. Consecutive waves on a court rotate between different groups.
- **🏓 Referee Scoring Console** — mobile-friendly score entry with +/− steppers. Referees are **pre-assigned** so no one officiates their own group or referees while they are playing (editable if needed). Filter by court, group, status, or "my matches."
- **📊 Standings** — live group tables (Win = 2 pts, Loss = 0), with the top 2 highlighted and a tie-breaker warning when points are level.
- **🎯 Qualification** — top 2 of each group auto-advance (12 teams) plus the best 4 of the six 3rd-place teams (wildcards) = 16.
- **🏆 Knockout Bracket** — Round of 16 → Quarterfinals → Semifinals → Final. Group winners are ranked by points and drawn against the weakest wildcards first; no two teams from the same group meet in the Round of 16.
- **☁️ Optional live sync** — add a free Firebase Realtime Database config and every phone shares scores in real time. Without it, the app runs fine in **local-only** mode (scores saved in that browser).

## Tournament format

| Stage | Detail |
|-------|--------|
| Group stage | 6 groups of 4, round robin — 36 matches, 3 games per team |
| Scoring | Win = 2 points, Loss = 0 |
| Advance | Top 2 per group (12) + best 4 third-place teams (4) = 16 |
| Knockout | Single elimination: Round of 16 → QF → SF → Final |
| Courts | 4 courts, 9 waves, ~20 min per match, start 4:00 PM |

Full rules are in [`docs/Pickleball_Tournament_2026_Rulebook.pdf`](docs/Pickleball_Tournament_2026_Rulebook.pdf).

## Running it

Just open `index.html` in any modern browser — that's it. To publish it so referees can reach it from their phones, host the single file (see below).

## Turning on live sync (optional)

By default the app is **local-only**: each device keeps its own scores. For shared, real-time scoring across phones:

1. Create a free Firebase project and a **Realtime Database** (test mode).
2. Copy your `firebaseConfig` values into the `FIREBASE_CONFIG` block near the top of the `<script>` in `index.html` (especially `databaseURL`).
3. Re-publish. The badge in the header turns to **● Live**.

Step-by-step: [`docs/SETUP_live_sync.md`](docs/SETUP_live_sync.md).

> Note: Firebase **web** config values are not secret (they identify the project, not authenticate it), so they are safe to commit. Just don't leave the database in open "test mode" long-term.

## Project structure

```
index.html                         The whole app (schedule, scoring, standings, qualify, bracket)
docs/
  Pickleball_Tournament_2026_Rulebook.pdf   Printable visual rulebook
  SETUP_live_sync.md                        How to enable Firebase live sync + hosting
  rulebook_source.html                      HTML source the rulebook PDF was rendered from
archive/
  original_draw_dashboard.html              Earlier draw-reveal dashboard (8-group format, superseded)
```

## Tech

Plain HTML, CSS, and vanilla JavaScript in one file. Optional [Firebase Realtime Database](https://firebase.google.com/docs/database) (loaded from CDN) for live sync. No frameworks, no build tools.

## License

[MIT](LICENSE) — free to use and adapt.

---

_Built for the Harisumiran Columbus Pickleball Tournament, June 2026._
