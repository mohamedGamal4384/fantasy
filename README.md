# Premier League 2025/26 Player & Team Analytics Dashboard

An interactive Power BI dashboard covering the 2025/26 Premier League season through gameweek 28: league table, team form, player profiles, every fixture, and a Team of the Week pitch view.

> **Unofficial fan project.** Not affiliated with, endorsed by, or connected to the Premier League. Club badges and player photos load from the league's public image URLs for portfolio and learning purposes only. Nothing from them is stored or redistributed here.

![Overview](Dashboard%20Previews/overview.png)

## Pages

| Page | What it shows |
|---|---|
| **Landing** | Entry page with season totals |
| **Overview** | Top 10 scorers, assists, goalkeepers, points, bonus and defenders, with flip cards that reveal the #1 player; goals and assists by position |
| **Teams** | League table, points progression, results split, goals for vs against, and a "last 5 matches" strip that reveals the opponent on hover |
| **Players** | Full profile for any player: KPIs, points, goals and assists by gameweek, and a gameweek table |
| **Matches** | Every fixture with scores, logos and results; highest scoring match; home vs away split |
| **Team of the Week** | The best XI of any gameweek on a pitch, with the top performer and points by line |

> Add one screenshot per page in `Dashboard Previews/` and link them here.

## How it is built

- **Power BI** for the report and data model, **Power Query** for the match-level tables, **DAX** for the measures.
- **Custom HTML/CSS/SVG inside DAX measures**, rendered by the *HTML Content* visual: hover animations, flip cards, SVG charts and the pitch view. Slicers, buttons and navigation stay as native Power BI visuals on top.
- **Figma** for the page layouts (1920 x 1080).

## Data model

Star schema: `Teams Dim`, `Players Dim`, `Gameweeks Dim` and `Date Dim` filter the player-gameweek fact table. Two match-level tables are built from fixture data:

- `Team Results` has one row per team per match (points, goals for/against, opponent).
- `Matches` has one row per match (home and away teams, score, date).

## What I learned

1. **Check what a column really means.** `team_id` in the player data is the player's *current* club, not the club he played for in that match. Summing it inflated some teams to 65 matches. I rebuilt the league table from fixture-level data and the totals finally matched reality.
2. **Verify before calling something a duplicate.** One team showed 29 matches instead of 28. It was a double gameweek (two different fixtures), not a duplicate.
3. **DAX gotchas.** A bare `COUNTROWS` inside `ADDCOLUMNS` ignores the row's filter, which made every donut slice equal until I wrapped it in `CALCULATE`.
4. **Design is part of the analysis.** If people cannot find the numbers, the dashboard does not work.

## Repository structure
