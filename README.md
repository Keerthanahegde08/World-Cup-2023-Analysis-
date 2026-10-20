# ICC Men's Cricket World Cup 2023 Analysis

Exploratory data analysis of all 48 matches of the 2023 ICC Men's Cricket World Cup, using Python. The project cleans the raw scorecard data, fixes several data-quality problems, and analyzes team results, venues, top performers and pressure situations.

## Project Objective

- Find out how teams performed, including wins, win percentage and wins by runs vs. wickets
- Compare batting first and chasing, overall and by venue
- Identify the top performer in each match and the tournament leaders
- Examine how teams fared when chasing big totals or defending small ones

## Dataset

Four CSV files, kept in the `data/` folder:

| File | Rows | Content |
|---|---|---|
| `batting_summary.csv` | 916 | Each batsman's innings: team, position, dismissal, runs, balls, 4s, 6s, strike rate |
| `bowling_summary.csv` | 574 | Each bowler's spell: overs, maidens, runs, wickets, economy |
| `match_schedule_results.csv` | 48 | Date, venue, teams, winner, scorecard URL |
| `world_cup_players_info.csv` | 151 | Player, country, batting and bowling style, playing role |

## Data Quality Fixes

The raw data had problems that change the results if left uncorrected. The code handles each one explicitly.

| Problem | Fix |
|---|---|
| **Matches 10 and 47** (both South Africa vs Australia) are loaded under both match numbers in the batting file, adding 40 duplicate rows | The mislabeled rows are removed and the code checks that no batsman appears twice in a match |
| **Innings order** is not in the data. The common assumption that `team_1` bats first is wrong (true in only 52% of matches) | Innings order is taken from the order each team appears in the batting file |
| **Match 33** (India vs Sri Lanka) lists Sri Lanka as the winner, but India made 337 and Sri Lanka were all out for 45 | Winner corrected to India. The code flags suspicious winners automatically |
| **No extras column**, so batsman runs understate team totals | Team totals are estimated from runs conceded by the opposition's bowlers (within a few runs of the real total) |
| **Rain-affected match** (match 35) | Detected and labeled as a DLS result |
| **Venue names** are inconsistent (e.g. two names for Dharamsala) | Standardized to city names, with stadium names added |

## What the Code Does

The notebook runs in 11 blocks:

1. Imports and loads the data
2. Standardizes column names and data types
3. Removes duplicated rows (matches 10 and 47)
4. Works out the real innings order and estimates team totals
5. Validates winners and detects DLS results
6. Team results: wins, win %, batting first vs. chasing, won by runs vs. wickets
7. Venue analysis: batting-first win % and average first-innings score
8. Best scorer and best bowler in each match
9. Tournament leaders: top 10 run scorers and wicket takers
10. Pressure situations: chasing 300+, defending under 200, results by first-innings total
11. Charts: team win %, batting-first win % by venue, top run scorers, top wicket takers

## Key Findings

**Teams**

| Team | Played | Won | Win % |
|---|---|---|---|
| India | 11 | 10 | 90.9 |
| Australia | 11 | 9 | 81.8 |
| South Africa | 10 | 7 | 70.0 |
| New Zealand | 10 | 5 | 50.0 |
| Pakistan, Afghanistan | 9 | 4 | 44.4 |
| England | 9 | 3 | 33.3 |
| Bangladesh, Netherlands, Sri Lanka | 9 | 2 | 22.2 |

- **Batting first won 23 of 48 matches (47.9%)** and chasing won 25 (52.1%).
- India won 5 matches by runs and 5 by wickets. Australia won 4 by runs and 5 by wickets.

**Venues** (only 3 to 5 matches each, so indicative)

- **Mumbai (Wankhede)** was the best venue for batting first: 4 of 5 wins, average first innings about 360.
- **Ahmedabad and Chennai** favored chasing the most: batting first won only 1 of 5 at each.
- Lucknow (Ekana) had the lowest average first-innings score (about 234).

**Individual performers**

- Most runs: Virat Kohli 765, Rohit Sharma 597, Quinton de Kock 594 (4 hundreds), Rachin Ravindra 578, Daryl Mitchell 552.
- Most wickets: Mohammed Shami 24, Adam Zampa 23, Dilshan Madushanka 21, Jasprit Bumrah 20, Gerald Coetzee 20.
- Best scorer in a match most often: Rohit Sharma and Daryl Mitchell (3 times each).
- Best bowler in a match most often: Gerald Coetzee and Mohammed Shami (4 times each).

**Pressure situations**

- Teams batting first won 85.7% of matches when scoring 300 to 349, and 90.9% when scoring 350+.
- Chasers won only 2 of 18 matches where the first-innings total was 300+ (one of those wins was a rain-affected DLS result).
- Teams batting first and scoring under 200 won 0 of 6 matches.
- Most 300+ totals: South Africa (5), then India, Australia and New Zealand (4 each).


## Tools Used

Python, pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook
