# Referee Scoring Site — Setup Guide

The file `referee_scoring.html` works two ways:

- **Local-only mode (no setup):** open it on a phone and it works immediately, but scores stay on that one device.
- **Live shared mode:** add a free Firebase config and host the file — every referee's phone shows the same scores in real time.

To get the live shared site that referees can use, do the two parts below. Total time ≈ 10 minutes.

---

## Part 1 — Turn on live sync (Firebase Realtime Database, free)

1. Go to **console.firebase.google.com** and sign in with a Google account. Click **Add project**, give it any name (e.g. `pickleball-2026`), and skip Google Analytics.
2. In the left menu choose **Build → Realtime Database → Create Database**. Pick any location, then select **Start in test mode** and enable.
3. Click the gear icon ⚙ next to *Project Overview* → **Project settings**. Scroll to **Your apps**, click the web icon **`</>`**, register an app (any nickname, no hosting needed yet). Firebase shows a `firebaseConfig` block — keep this open.
4. Open `referee_scoring.html` in any text editor. Near the top of the `<script>` section find:

   ```js
   const FIREBASE_CONFIG = {
     apiKey:        "PASTE_API_KEY",
     authDomain:    "PASTE_PROJECT.firebaseapp.com",
     databaseURL:   "PASTE_DATABASE_URL",
     projectId:     "PASTE_PROJECT_ID"
   };
   ```

   Replace each value with the matching value from your `firebaseConfig`. The **`databaseURL`** is the important one — it looks like `https://pickleball-2026-default-rtdb.firebaseio.com`. (If your config doesn't show a `databaseURL`, copy it from the Realtime Database page; it's the URL shown at the top of the data view.)
5. Save the file. When you open it now, the top-right badge should read **● Live** instead of ● Local.

> Test-mode rules allow anyone with the link to read/write for 30 days — perfect for a one-day event. Don't reuse this database for sensitive data afterward.

---

## Part 2 — Host the file so referees can open it on their phones

Pick whichever is easiest:

**Option A — Netlify Drop (fastest, no account needed to start)**
1. Go to **app.netlify.com/drop**.
2. Drag `referee_scoring.html` onto the page. (Tip: rename it to `index.html` first so the URL is clean.)
3. Netlify gives you a public link like `https://random-name.netlify.app`. Share it with all referees.

**Option B — Firebase Hosting** (same project)
- Install the Firebase CLI, run `firebase init hosting`, drop the file (as `index.html`) into the `public` folder, then `firebase deploy`.

**Option C — GitHub Pages**
- Put the file in a public repo as `index.html`, enable Pages in repo settings, share the Pages URL.

---

## Using it on the day

- Each referee opens the link, types **their name** in the top box, and taps **⭐ Mine** to see only matches assigned to them (assign refs in each match card's **Ref** field).
- Tap **−/+** or type to enter scores. The winner is highlighted automatically and standings update live.
- **Standings** tab shows each group; ①② are the auto-qualifiers. A ⚠ appears if a points tie needs a tie-breaker match.
- **Qualify** tab ranks the six 3rd-place teams and picks the best 4. If there's a tie at the cut, play the tie-breaker, then tick the 4 teams that advance.
- **Bracket** tab seeds the 16 qualifiers (by points, then point-difference) into the Round of 16 and auto-advances winners to the Final.
- **Setup** tab has Export/Import/Reset tools and shows your live-sync status.

## Format recap (built in)
- 6 groups of 4 → round robin, **36 group matches** (3 per team). Win = 2 pts, loss = 0.
- Top 2 of each group auto-advance (12) + best 4 of the six 3rd-place teams (4) = **16-team Round of 16** → QF → SF → Final.
