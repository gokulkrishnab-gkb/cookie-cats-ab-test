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
- **7-day retention (primary):** 19.02% with the gate at level 30 vs 18.20% at level 40, a difference of 0.82 percentage points (95% CI 0.31 to 1.33; two-proportion z-test p = 0.0016). Relative drop: 4.3%.
- **Business scale:** about 820 fewer players active at day 7 per 100,000 installs (plausible range 310 to 1,330).
- **1-day retention (secondary):** 44.82% vs 44.23% (p = 0.074), not statistically significant at the 5% level.
- *In progress: bootstrap, power analysis, peeking simulation, multiple-testing correction and the ship decision.*
- **Bootstrap check:** resampling gives the same 95% interval for the 7-day difference as the formula (0.31 to 1.34 points), so the result does not depend on a normal approximation.
- **Engagement:** median game rounds are 17 vs 16 (bootstrap interval for the difference [0, 1]), so the retention gap is not accompanied by a clear change in typical playing volume.

![Bootstrap distribution](charts/bootstrap_retention7.png)

- **Power:** about [N] players per group were needed to detect the observed gap at 80% power, against about 45,000 in the experiment. The test could reliably detect differences of about [X] points or more.

## Files
| File | What it does |
|---|---|
| `ab_test.ipynb` | Analysis notebook |

## How to reproduce
```
pip install -r requirements.txt
```