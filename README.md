# Cookie Cats A/B Test: does moving the gate from level 30 to 40 hurt retention?

## Business problem
A mobile game (Cookie Cats) moved its first gate from level 30 to level 40 for half of new players. Should the product team ship the change?

## Data
About 90k players from the Kaggle "Mobile Games A/B Testing - Cookie Cats" dataset: player ID, version (`gate_30` or `gate_40`), game rounds in the first 14 days, and whether the player returned after 1 and 7 days. The data is not included in this repo.

## Experiment design
- **Primary metric:** 7-day retention. **Secondary:** 1-day retention. **Supporting:** game rounds.
- **H0:** retention is the same in both versions. **H1:** it differs (two-sided).

## Data checks
- No missing values and no duplicate user IDs.
- Group sizes are 45,489 (gate_40) and 44,700 (gate_30). The 50/50 split test gives p = 0.0086, borderline under the usual 0.001 alert threshold, so it is noted as a limitation.
- One gate_30 player has 49,854 rounds, likely a bot, so rounds comparisons use the median.

## Results
*In progress: statistical tests, confidence intervals, bootstrap and power analysis.*

## Recommendation
*Coming after the analysis.*

## Files
| File | What it does |
|---|---|
| `ab_test.ipynb` | Analysis notebook |

## How to reproduce
```
pip install -r requirements.txt
```