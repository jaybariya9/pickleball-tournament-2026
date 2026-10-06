# Columbus Pickleball 2026

A small web app I put together with help of Claude to run our 24 team doubles tournament. It holds the match schedule across 4 courts, lets referees enter scores from their phones, and keeps the standings, qualifiers, and knockout bracket updated as games finish. The whole thing is a single file, `index.html`. There is no server to run and nothing to install, so you can just open it in a browser.

Live site: https://jaybariya9.github.io/pickleball-tournament-2026/

## What it does

**Match schedule.** 6 groups of 4 play a round robin on 4 courts across 9 waves, starting at 4:00 PM with about 20 minutes per match. Groups A, C and E play on Courts 1 and 2, while B, D and F play on Courts 3 and 4, so every team stays on the same pair of courts the whole time. Back to back matches on a court rotate between different groups.

**Referee scoring.** Score entry is built for phones, with plus and minus buttons. Referees are assigned ahead of time so nobody officiates their own group or referees while their own team is playing, and you can change any assignment on the spot. You can filter the list by court, group, status, or just your own matches.

**Standings.** Group tables update as scores come in. A win is 2 points and a loss is 0. The top two in each group are highlighted, and a note appears if teams are tied and need a playoff.

**Qualifiers.** The top two from each group go through automatically, which is 12 teams. The 4 best third place teams fill the last spots, for 16 total.

**Bracket.** Round of 16 through the final. Group winners are ranked by points and drawn against the weakest wildcards first, and two teams from the same group cannot meet in the Round of 16.

**Live sync (optional).** Add a free Firebase config and every phone shares the same scores in real time. Without it, each device just keeps its own copy.

## Format at a glance

| Stage | Detail |
|-------|--------|
| Group stage | 6 groups of 4, round robin. 36 matches, 3 games per team |
| Scoring | Win = 2 points, Loss = 0 |
| Advancing | Top 2 per group (12) plus the 4 best third place teams, 16 total |
| Knockout | Single elimination: Round of 16, Quarterfinals, Semifinals, Final |
| Courts | 4 courts, 9 waves, about 20 minutes per match, start 4:00 PM |

The full rules are in [docs/Pickleball_Tournament_2026_Rulebook.pdf](docs/Pickleball_Tournament_2026_Rulebook.pdf).

## Running it

Open `index.html` in any modern browser and you are set. To let referees use it from their phones, host that one file somewhere (GitHub Pages is the easy option) and share the link.

## Turning on live sync

Out of the box, each device keeps its own scores. For shared scoring across phones:

1. Create a free Firebase project with a Realtime Database in test mode.
2. Copy your `firebaseConfig` values into the `FIREBASE_CONFIG` block near the top of the script in `index.html`, especially `databaseURL`.
3. Publish again. The badge in the header changes to show it is live.

The step by step version is in [docs/SETUP_live_sync.md](docs/SETUP_live_sync.md).

A quick note on safety: Firebase web config values are not secret, so they are fine to keep in the repo. Just do not leave the database open in test mode forever.

## What is in here

```
index.html                         The whole app (schedule, scoring, standings, qualifiers, bracket)
docs/
  Pickleball_Tournament_2026_Rulebook.pdf   Printable rulebook
  SETUP_live_sync.md                        How to turn on Firebase sync and host the file
  rulebook_source.html                      The HTML the rulebook PDF was made from
archive/
  original_draw_dashboard.html              An earlier draw dashboard from the 8 group version
```

## Built with

Plain HTML, CSS and JavaScript in one file. Firebase Realtime Database is optional and only used for live sync. No frameworks and no build step.

## License

MIT, so use it and change it however you like.
