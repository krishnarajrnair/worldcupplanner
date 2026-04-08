# FIFA World Cup 2026 Tracker & Planner

A single-file, offline-capable web app for tracking the 2026 FIFA World Cup — enter group results, watch the bracket auto-fill, and plan which matches you're attending or watching.

No server, no login, no dependencies. Just open `index.html` in a browser, or visit the live app at **https://krishnarajrnair.github.io/worldcupplanner**.

---

## Getting Started

1. Download or clone this repository
2. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari)
3. All data is saved automatically in your browser's **localStorage** — it persists across sessions on the same device

> **Note:** The timezone selector and most features work fine from a local file. The file can also be served from any static host (GitHub Pages, Netlify, etc.).

---

## Features

### Overview Tab
- **Tournament at a Glance** — cards showing total teams, matches, groups, and venues; click any card to expand detail
- **Format** — quick visual of the tournament structure from Group Stage to Final
- **Host Venues** — all 16 stadiums across USA, Canada, and Mexico; click to expand the match list per venue
- **Import / Export** — CSV tools for results and plans (see [Data section](#data-import--export))

### Groups & Bracket Tab

#### Group Stage
- Displays all 12 groups (A–L) with live standings
- Click any match row to enter or edit a score
- Standings update instantly: top 2 advance (green), 3rd place highlighted in gold
- **3rd Place Standings & R32 Draw** panel at the bottom shows all 12 third-placed teams ranked by FIFA tiebreakers, which 8 qualify, and which Round of 32 match each is mapped to — using the official FIFA 495-scenario lookup table

#### Knockout Bracket
- Auto-fills from group results as you enter them
- Full bracket from Round of 32 through the Final
- Click any match to enter a score; the winner advances automatically
- Unconfirmed teams show in a dimmed "projected" style
- Hover over any match to see which teams could potentially play there

### My Planner Tab
- Add matches you plan to **Attend** (in-person), **Watch** (on TV/stream), or are **Considering**
- Link a plan to a specific match using the dropdown — the app keeps the match name live, so as bracket results come in (e.g. "W79 (Argentina)") your planner updates automatically
- Track: tickets, cost, seat reference, travel details, attendees, and notes
- **View Match** button navigates directly to the match in the bracket or group stage

---

## Entering Results

### Group Stage
1. Go to **Groups & Bracket → Group Stage**
2. Select a group tab (A–L)
3. Click any match row to open the score modal
4. Enter home and away scores, then click **Save**
5. Standings and the knockout bracket update immediately

### Knockout Stage
1. Go to **Groups & Bracket → Knockout Bracket**
2. Click any match card
3. Enter scores (must have a winner — draws not allowed in knockout)
4. The winner auto-advances to the next round

---

## Timezone

All kickoff times are stored in UTC and displayed in your chosen timezone. Use the **🌐 timezone selector** in the top navigation bar to switch between:

| Label | Timezone |
|---|---|
| ET | America/New_York |
| CT | America/Chicago |
| MT | America/Denver |
| PT | America/Los_Angeles |
| BRT | America/Sao_Paulo |
| GMT/BST | Europe/London |
| CET/CEST | Europe/Paris |
| GST | Asia/Dubai |
| IST | Asia/Kolkata |
| SGT | Asia/Singapore |
| JST | Asia/Tokyo |
| AEST | Australia/Sydney |

Your selection is saved and remembered across sessions.

---

## Data Import / Export

All import/export is via CSV files. Access from the **Overview tab → Data** section.

### Results CSV
Export the full group stage results. Can be re-imported to restore or share scores.

| Column | Description |
|---|---|
| Game# | Official FIFA match number (1–104) |
| Group/Round | e.g. "Group A", "Round of 32" |
| Date | Match date |
| Home Team | Home team name |
| Away Team | Away team name |
| Score Home | Goals scored by home team |
| Score Away | Goals scored by away team |
| Venue | Stadium name |

### Plans CSV
Export your personal planner entries. Can be re-imported on another device.

| Column | Description |
|---|---|
| GameNum | Official FIFA match number — used to re-link the plan to the correct match on import |
| Match | Match description |
| Round | Tournament round |
| Date | Your planned date |
| Venue | Venue name |
| Status | `attending`, `watching`, or `planning` |
| Tickets | Number of tickets |
| Cost | Total cost in USD |
| Attendees | Comma-separated names |
| TicketRef | Ticket reference / seat info |
| Travel | Travel notes |
| Notes | Any other notes |

> **Re-linking on import:** The `GameNum` column is the official FIFA match number (publicly known, 1–104). When importing a plans CSV, the app uses this number to automatically re-establish the live link to the correct match — so the match name updates as the bracket progresses.

---

## 3rd Place Draw Logic

FIFA 2026 has 12 groups; only the best 8 third-placed teams advance to the Round of 32. The app includes the complete official FIFA mapping table (all 495 combinations of which 8 groups can produce advancing third-place teams) and automatically determines:

- Which 8 third-place teams qualify based on points → goal difference → goals scored
- Which Round of 32 match each third-place team is assigned to (following FIFA's published draw rules)

This updates live as you enter group results.

---

## Data Storage

All data is stored in **browser localStorage** under these keys:

| Key | Contents |
|---|---|
| `wc26_groups` | Group stage scores and standings |
| `wc26_bracket` | Knockout bracket results |
| `wc26_plans` | Your planner entries |
| `wc26_tz` | Your timezone preference |
| `wc26_version` | Schema version (used to reset stale data on updates) |

Data is **local to your browser and device** — it is never sent anywhere. To transfer to another device, use the CSV export/import tools.

---

## Browser Compatibility

Works in any modern browser that supports ES6+ and the `Intl.DateTimeFormat` API:

- Chrome 80+
- Firefox 75+
- Edge 80+
- Safari 14+

---

## Tournament Data

- **Teams:** 48 teams across 12 groups (A–L)
- **Matches:** 104 total (72 group stage + 16 R32 + 8 R16 + 4 QF + 2 SF + 1 3rd place + 1 Final)
- **Venues:** 16 stadiums across USA (11), Canada (2), Mexico (3)
- **Kickoff times:** All times sourced from the official FIFA 2026 schedule (EDT/UTC-4 base)
- **Game numbers:** Official FIFA match numbers (#1–#104)
