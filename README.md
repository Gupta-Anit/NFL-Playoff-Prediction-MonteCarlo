# NFL Playoff Prediction (Monte Carlo)

Input datasets for a planned Monte Carlo simulation of the NFL playoffs, used to
estimate each team's probability of winning the Super Bowl.

> **Note:** This repository currently contains only the input datasets. The
> Monte Carlo simulation code is not yet committed (see [Status](#status)).

## Overview

The goal of this project is to simulate the NFL playoff bracket many thousands
of times via Monte Carlo, advancing teams round by round according to estimated
matchup win probabilities, and to aggregate the results into a championship
probability for each team. The datasets in this repository provide the three
inputs such a simulation needs: the playoff field and seeding, pairwise matchup
win probabilities, and team/conference metadata.

## Data

### `Playoff_seeds.csv`

The playoff field: the seeded teams in each conference.

| Column | Meaning |
| --- | --- |
| `Conference` | Conference the team belongs to (`AFC` or `NFC`) |
| `Seed` | Playoff seed within the conference (1 = top seed) |
| `Team` | Team name (e.g. `Chiefs`) |
| `Wins` | Regular-season wins |
| `Losses` | Regular-season losses |
| `Percent` | Regular-season win percentage (e.g. `75.00%`) |

### `playoff_games.csv`

Pairwise win probabilities for potential playoff matchups, keyed by team
abbreviation.

| Column | Meaning |
| --- | --- |
| `home.team` | Home team abbreviation (e.g. `KC`) |
| `away.team` | Away team abbreviation (e.g. `DAL`) |
| `Avg.Prob` | Estimated probability that `home.team` beats `away.team` |

### `team_conf.csv`

Team reference/metadata, including division and conference assignments and team
colors (useful for joining abbreviations to full names and for plotting).

| Column | Meaning |
| --- | --- |
| `team` | Full team name (e.g. `Baltimore Ravens`) |
| `abbr` | Team abbreviation (e.g. `BAL`) |
| `primary` | Primary team color (hex) |
| `secondary` | Secondary team color (hex) |
| `tertiary` | Tertiary team color (hex) |
| `quaternary` | Quaternary team color (hex) |
| `division` | Division (e.g. `AFC North`) |
| `conference` | Conference (`AFC` or `NFC`) |

## Status

- **Datasets present:** `Playoff_seeds.csv`, `playoff_games.csv`, and
  `team_conf.csv` are committed and documented above.
- **Simulation code not yet committed:** the Monte Carlo simulation described
  below has not been added to this repository. No results are produced yet.

## Planned approach

A standard Monte Carlo bracket simulation over many trials (e.g. 10,000+):

1. Build the bracket from `Playoff_seeds.csv`, pairing teams by seed within each
   conference (wild-card, divisional, conference championship, then Super Bowl).
2. For each game in a simulated bracket, look up the matchup win probability in
   `playoff_games.csv` (using abbreviations from `team_conf.csv` to bridge the
   team naming) and draw the winner with a random sample against that
   probability.
3. Advance winners round by round until a champion is decided.
4. Repeat across all trials and tally how often each team wins, yielding an
   estimated championship probability per team.

## License

Released under the [MIT License](LICENSE).
