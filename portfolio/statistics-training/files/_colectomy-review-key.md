# Review key: Surgical approach and recovery after colectomy

Scenario `colectomy-recovery`, seed 81130, n = 200.

## Accepted methods

- **Linear regression (ANCOVA) on QoR-15 with approach and baseline covariates** (preferred): Baseline covariates improve precision; randomization already handles confounding.
- **Two-sample t-test (or Wilcoxon) comparing QoR-15 by approach** (acceptable): Valid in a randomized trial, but less precise because baseline covariates are ignored.
- **Any model that includes length_of_stay as a covariate** (flawed): Length of stay is a consequence of the approach; including it biases the approach estimate.

## Variable decisions

| Variable | Decision | Reason |
|---|---|---|
| `approach` | include | Randomized treatment of interest. |
| `age` | include | Measured before surgery; adjust for precision. |
| `bmi` | include | Measured before surgery; adjust for precision. |
| `diabetes` | include | Measured before surgery; adjust for precision. |
| `length_of_stay` | exclude | Measured after surgery and affected by the approach. It is part of how the approach affects recovery, not a baseline characteristic. |

## Wrinkles

- **A3_post_treatment**: Length of stay is measured after surgery and depends on the approach (laparoscopic patients go home about 2 days sooner) and on complications, which also lower QoR-15. Adjusting for it distorts the approach effect.

Checks on this draw:

- PASS (A3_post_treatment): length_of_stay differs across approach (|SMD| 1.09, need >= 0.2); adding it shifts approach by 4.07 SE (need >= 1.5)

## Expected findings

- Laparoscopic surgery improves QoR-15 by about 7 points.
- Adding length_of_stay to the model shrinks or even reverses the approach effect.
- Randomization balanced the baseline covariates.

## This draw vs. the truth (outcome units)

Intended model: `qor15_30d ~ approach + age + bmi + diabetes`.

| Term | True | Estimate | 95% CI | p | Label |
|---|---:|---:|---|---:|---|
| approach[Laparoscopic] | 7 | 6.618 | 3.242 to 9.994 | 0.000151 | detected |
| age | -0.25 | -0.406 | -0.582 to -0.231 | 8.41e-06 | detected |
| bmi | -0.4 | -0.354 | -0.709 to 0.001 | 0.0503 | MISSED: real effect not significant (limited power) |
| diabetes[Yes] | -5 | -7.948 | -11.991 to -3.905 | 0.000144 | detected |

## What the trap gives

Results a student would get by falling into the wrinkle, for comparison.

| Model | Term | Estimate | 95% CI | p |
|---|---|---:|---|---:|
| adds `length_of_stay` | approach[Laparoscopic] | -0.354 | -3.575 to 2.868 | 0.829 |

## For the reveal

A correct analysis of this dataset will show the following, which differ from the truth by chance. Credit the analysis, then explain:
- `bmi`: missed: real effect not significant (limited power).

## Descriptive summaries

What an unadjusted or table-based analysis of this dataset shows.

**approach** (unadjusted one-way ANOVA p = 0.000221)

| approach     |   n |   mean |    sd |
|:-------------|----:|-------:|------:|
| Open         | 100 | 100.29 | 11.63 |
| Laparoscopic | 100 | 107.25 | 14.38 |

**diabetes** (unadjusted one-way ANOVA p = 0.000561)

| diabetes   |   n |   mean |    sd |
|:-----------|----:|-------:|------:|
| No         | 156 | 105.5  | 13.16 |
| Yes        |  44 |  97.64 | 13.03 |

**Balance across `approach`**

| Variable | By group | Max abs SMD |
|---|---|---:|
| `age` | Open: 64.02, Laparoscopic: 61.74 | 0.24 |
| `bmi` | Open: 28.84, Laparoscopic: 29.60 | 0.16 |
| `diabetes` | Open (% Yes): 0.20, Laparoscopic (% Yes): 0.24 |  |
