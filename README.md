# Mettlestate × Marvel Snap — Public Leaderboard

A fully Marvel Snap–themed, mobile-first, read-only leaderboard for the Mettlestate Marvel Snap League. No backend — reads straight from `data/league-data.json`, which the admin app keeps in sync.

## What's new in this redesign

This isn't a recolored EA FC leaderboard anymore — it's built around Marvel Snap's own identity: Cubes, Snaps, and comic-book presentation.

- **Comic-book visual language** — Anton/Bebas Neue display type, JetBrains Mono for stats, halftone-dot textures, a red/gold gradient lifted straight from the new player registration page, and a subtle animated **Cube Rain** falling behind the content (rotated squares drifting down like Snap's Cubes)
- **Holographic Champion card** — the #1 podium spot gets a shimmer sweep animation and a bobbing crown icon, like a foil trading card
- **Rank gems** — positions 1–3 get gold/silver/bronze diamond badges instead of plain numbers, on both the mobile cards and desktop table
- **Win-streak flames** — any player on a 3+ game win streak gets a 🔥 flame badge with their streak count, right next to their name
- **New "Cube Leaders" tab** — a season-standouts panel separate from the main standings: Most Cubes Won, Best Win Rate, On Fire (longest active streak), Best Cube Difference
- **Snap Impact tags in Match History** — every result is auto-labelled by its final Cube count: `Retreat Win` (1 Cube), `Snap Win` (2), `Double Snap` (4), `MEGA SNAP` (8+) — so big wins visually pop
- **Rotating hero tagline** — a strip of flavour text up top that cycles every few seconds
- **Pull-to-refresh** on mobile, unchanged from before, still works

## Data contract (unchanged)

Still reads `data/league-data.json` in the same shape the admin app already writes:

```json
{
  "players": [{ "name": "...", "username": "...", "played": 0, "wins": 0, "draws": 0, "losses": 0, "points": 0, "gf": 0, "ga": 0, "form": [], "postponements": 20, "suspended": false }],
  "results": [{ "home": "...", "away": "...", "homeGoals": 0, "awayGoals": 0, "date": "YYYY-MM-DD" }],
  "updatedAt": "ISO timestamp",
  "matchesPlayed": 0
}
```

`gf`/`ga` are each player's total Cubes won / Cubes lost across the season. `homeGoals`/`awayGoals` on a result are the two players' final Cube counts for that match — the field names are kept from the original engine for compatibility with the admin app, but they mean Cubes, not goals.

## Setup

1. Push this repo to GitHub, enable **Pages** (Settings → Pages → Deploy from branch → main / root)
2. Your leaderboard is live at `https://{username}.github.io/{repo}/`
3. The admin app writes to `data/league-data.json` in this repo automatically via its GitHub Sync — no manual editing needed

## File structure

```
/
├── index.html              ← Everything: markup, styles, and script in one file
├── data/
│   └── league-data.json    ← Synced automatically by the admin app
└── .github/workflows/
    └── static.yml           ← GitHub Pages deploy workflow
```
