# Matchmatics: Fusion of Math and Statistics in Sports

A centralized sports database and analytics dashboard that brings **ODI cricket, FIFA football, and NBA basketball** data together in one PostgreSQL database (`sportsdb`), with a React web app on top for exploring it.

Built as a team project for a database course at the University at Buffalo, SUNY.

---

## 1. What is the project?

Sports generate huge amounts of data, but analysts, coaches, and fans often end up working with disconnected Excel sheets and one-off scripts, especially across multiple sports. Matchmatics solves this by putting three sports into a single, well-designed relational database and giving users an easy interface to explore it.

- **One database, three sports.** A central `Sports` table links the ODI cricket, FIFA, and NBA schemas, so records from every sport are tied to the right sport.
- **Query and update support.** The schema is in BCNF and supports joins, indexing, stored procedures, and transactional updates.
- **Dashboard instead of a news-page look.** Users pick a sport, land on a dashboard with visualizations of its statistics, and can run queries against that sport's tables to pull specific data.

**Example questions it can answer**

| Sport | Example query |
|---|---|
| Cricket | Top run scorers across all ODIs, partnerships of 200+ runs, bowlers with the best economy |
| FIFA | Players with the most World Cup tournaments, appearances by team and position, starters vs. substitutes |
| NBA | Head-to-head records between two teams, highest-scoring games, first pick of each draft round |

**Datasets**

- FIFA: [football.db / openfootball](https://openfootball.github.io/docs/json-api-intro.html) (`players`, `player_appearances`, `squads`)
- NBA: [Kaggle NBA Database](https://www.kaggle.com/datasets/wyattowalsh/basketball/data) (`player`, `draft_history`, `game`, `game_summary`, `other_stats`, `line_score`)
- ODI Cricket: [Kaggle ODI Matches Historical Data](https://www.kaggle.com/datasets/bhuvaneshprasad/odi-matches-historical-data-since-1971) (`matches`, `batting`, `bowling`, `partnerships`, `fall_of_wickets`, `cric_players`)

---

## 2. Tech stack

| Layer | Technology |
|---|---|
| Frontend | React, TypeScript, Bootstrap, Tailwind CSS |
| Backend | Node.js (connects the app to the database) |
| Database | PostgreSQL |
| Database design | ER modelling, relational schema, BCNF normalization |
| Performance | B-tree and composite indexes, `pg_trgm` + GIN indexes for text search, `EXPLAIN` analysis |
| Database logic | Stored procedures, transactions with rollback, trigger-based failure logging |

---

## Preview: FIFA dashboard

<p align="center">
  <img src="screenshots/fifa-dashboard.gif" alt="Matchmatics FIFA dashboard" width="650">
</p>

<p align="center"><sub>
The full database is several 5.8 GB (NBA, FIFA, and ODI cricket), so it isn't hosted and there is no live demo. The preview above was recorded running locally against the full database.
</sub></p>

---

## 3. My contribution

This was a three-person team project. My work covered the **FIFA side of the database** and the **entire frontend**.

### FIFA data and database work

- Worked on all of the FIFA datasets end to end, including the `players`, `player_appearances`, and `squads` tables.
- Designed the FIFA relational schema (keys, foreign keys to `Sports`, and attributes like positions, tournaments, starter/substitute flags) and checked it against BCNF.
- Wrote and ran the FIFA SQL queries, including joins filtered by `sports_id`, `ORDER BY` leaderboards (e.g., most tournaments played), `GROUP BY` aggregations, and subqueries.
- Optimized FIFA queries with indexing (composite indexes on `player_appearances`, trigram/GIN indexes for player name and position search) and compared plans with `EXPLAIN`.

### Frontend (built entirely by me)

- Built the full React + TypeScript web app.
- Designed the sport-selection flow, so users choose cricket, football, or basketball and are taken to that sport's dashboard.
- Built the dashboard visualizations (stat cards, line, pie, and bar charts) that surface statistics from the database.
- Built the query interface that lets users fetch data from each sport's tables.
- Styled the UI with Bootstrap and Tailwind CSS.

---

## Team

- Anchal Daga
- Shruti Kumari
- V L Sivasai Mani Harshith Bhattaram

*Course instructor: Prof. Shamshad Parvin. TA: Vamshi Krishna Kyatham.*
