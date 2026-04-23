# Premier League 2024/25 — Title Race Visualiser

An interactive animated bump chart tracking the position of all 20 Premier League clubs across every matchweek of the 2024/25 season, built entirely from raw StatsBomb event data.

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![Plotly](https://img.shields.io/badge/Plotly-5.x-informational?style=flat-square&logo=plotly)
![Data](https://img.shields.io/badge/Data-StatsBomb-red?style=flat-square)
![Colab](https://img.shields.io/badge/Platform-Google%20Colab-orange?style=flat-square&logo=google-colab)

---

## 🔴 Live Demo

**[▶ Open Interactive Visualisation](https://leiderip.github.io/Premier-League-2024-25-Title-race/pl_position_race.html)**

---

## Overview

This project processes **380 match CSV files** from StatsBomb's event-level dataset and builds a fully interactive league standings animation — from raw events to polished visualisation — with no pre-aggregated data.

The chart shows how each club's league position evolved week by week, revealing the full narrative of the title race, the relegation battle, and the European qualification fight in a single interactive view.

---

## Features

- **Animated bump chart** — 38-matchweek position race with Play / Pause control and a matchweek slider
- **Team badges** — Premier League SVG crests embedded as base64 (no external requests, CORS-free)
- **Dark / Light theme toggle** — switch between dark navy and clean white with a single click
- **Zone bands** — visual markers for Champions League, Europa League, Conference League, and Relegation zones
- **Rich tooltips** — hover any point to see Position, Points, W-D-L, GF, GA, and GD for that matchweek
- **Fully self-contained HTML** — the exported file runs offline in any modern browser

---

## Data Pipeline

| Step | Description |
|---|---|
| Goal extraction | Shot + Goal outcome, deduplicated on event id |
| Own goal attribution | 'Own Goal For' events credited to beneficiary team |
| Match result calculation | W/D/L and points per match |
| Cumulative standings | Built for every matchweek (Pts → GD → GF tiebreak) |
| Plotly animated figure | 38 frames, one per matchweek |
| HTML export + CSS inject | Smooth logo transitions, font loading, theme toggle |

---

## Key Technical Decisions

| Challenge | Solution |
|---|---|
| Freeze-frame rows duplicating goal events | drop_duplicates('id') before counting |
| Team name mismatch between filename and data | First-word matching against team_name column |
| Logo CORS block in browser | Downloaded and embedded as base64 data URIs |
| Logos snapping between frames | CSS transition injected into exported HTML |
| Tottenham SVG tighter viewBox | Per-team sizex/sizey override dictionary |
| Zone labels overlapping team logos | Moved to paper-coordinate legend panel |

---

## Stack

| Tool | Purpose |
|---|---|
| pandas | Event data loading, goal aggregation, standings computation |
| plotly | Animated interactive chart, frame-by-frame layout |
| requests + base64 | Logo fetching and embedding |
| pathlib + re | Batch file discovery and filename parsing |
| Google Colab | Development environment |

---

## How to Run

1. Upload the match CSVs and logos CSV to Google Drive
2. Open the notebook in Google Colab
3. Update the three paths in **Cell 2**
4. Run all cells — processing ~380 files takes roughly 3-5 minutes
5. Open the exported HTML in any browser

> **Note:** The 380 match CSVs are not included due to file size. Source data available from [StatsBomb Open Data](https://github.com/statsbomb/open-data).

---

## About

Built as part of a data analytics portfolio during an MSc in Applied Performance Analysis at the **University of Essex**.

The project demonstrates end-to-end data work: raw event ingestion, domain-specific logic (goal attribution, tiebreak rules), iterative visual design, and front-end polish — all within a single reproducible notebook.

---

*Data © StatsBomb. Club badges © Premier League. Project code MIT licensed.*
