# Academic Stress Student Project

This project studies the relationship between study load, sleep quality, social support, and student stress level using statistical models and sensitivity analyses.

## Research question

Are study load, sleep quality, and social support associated with students' stress levels?

The dataset is observational. Therefore, the results describe associations and should not be interpreted as causal effects.

## Data

The project uses `StressLevelDataset.csv`.

The dataset contains 1,100 observations and 21 variables.

The main variables used in this analysis are:

| Variable | Role | Observed values |
| --- | --- | --- |
| stress_level | Outcome | 0 = Low, 1 = Medium, 2 = High |
| study_load | Predictor | 0 to 5 |
| sleep_quality | Predictor | 0 to 5 |
| social_support | Predictor | 0 to 3 |

The data checks found no missing values and no exact duplicate rows.

The original data file is kept unchanged inside the `data` folder.

## Analysis

The main model is ordinal logistic regression because stress level contains three ordered categories.

The analysis also includes:

* Descriptive summaries and visualizations
* Cross tabulations
* Chi square tests
* Cramer's V
* Spearman correlation
* Variance inflation factors
* Ordinal logistic regression
* Threshold specific logistic models
* Multinomial logistic regression
* Alternative coding of ordinal predictors
* Bayesian multinomial logistic regression

The additional models were used to examine assumptions and determine whether the main conclusions changed under different modeling choices.

## Main ordinal model

The adjusted ordinal logistic regression produced the following estimates:

| Predictor | Odds ratio | 95% confidence interval | p value |
| --- | ---: | ---: | ---: |
| Study load | 2.16 | 1.85 to 2.51 | < 0.001 |
| Sleep quality | 0.31 | 0.27 to 0.36 | < 0.001 |
| Social support | 0.45 | 0.38 to 0.53 | < 0.001 |

Higher study load was associated with higher stress.

Higher sleep quality was associated with lower stress.

Higher social support was also associated with lower stress in the ordinal model.

## Checking the ordinal model

The proportional odds assumption was examined using separate threshold models.

The patterns for study load were reasonably similar across thresholds.

Sleep quality showed some differences in effect size.

Social support showed a much larger difference between thresholds.

This suggested that a single proportional odds estimate may not describe the social support relationship adequately.

## Multinomial sensitivity analysis

A multinomial logistic regression was therefore fitted using Low stress as the reference category.

For Medium stress compared with Low stress:

| Predictor | Odds ratio | 95% confidence interval |
| --- | ---: | ---: |
| Study load | 1.89 | 1.54 to 2.32 |
| Sleep quality | 0.33 | reported in the notebook |
| Social support | 0.98 | 0.78 to 1.22 |

Social support did not clearly distinguish Medium stress from Low stress after adjustment.

For High stress compared with Low stress:

| Predictor | Odds ratio |
| --- | ---: |
| Study load | 3.17 |
| Sleep quality | 0.18 |
| Social support | 0.17 |

The association involving social support was much stronger for High stress than for Medium stress.

## Alternative coding of the predictors

Study load, sleep quality, and social support are ordinal scores.

The main models treated these scores as numeric predictors.

To examine whether the conclusions depended on this choice, each predictor was also examined using categorical coding.

The Study load model converged and broadly preserved the positive association with stress, although the effects differed across score levels.

The Sleep quality model also converged, but the pattern across categories was not completely linear.

The categorical Social support model did not converge.

Inspection of the data showed several empty combinations of Social support and Stress level.

For example:

| Social support | Low | Medium | High |
| ---: | ---: | ---: | ---: |
| 0 | 25 | 36 | 27 |
| 1 | 48 | 22 | 342 |
| 2 | 0 | 142 | 0 |
| 3 | 300 | 158 | 0 |

These empty cells produced separation and unstable estimates in the standard categorical multinomial model.

The coefficients from that model were therefore not interpreted.

## Bayesian sensitivity analysis

A Bayesian multinomial logistic regression was fitted as an additional sensitivity analysis.

Low stress was used as the reference outcome.

The predictors were standardized before model estimation.

Weakly informative prior distributions were used for the regression coefficients.

The sampling diagnostics were satisfactory.

All reported R hat values were approximately 1.00 and no divergent transitions were observed.

### Bayesian results

The odds ratios below correspond to a one standard deviation increase in each predictor.

| Predictor | Medium vs Low | High vs Low |
| --- | ---: | ---: |
| Study load | 2.32 | 4.60 |
| Sleep quality | 0.19 | 0.07 |
| Social support | 0.99 | 0.16 |

The Bayesian results supported the main positive association between study load and stress.

Higher sleep quality remained strongly associated with lower stress.

Social support again showed different relationships across stress categories.

For Medium stress compared with Low stress, the estimated odds ratio was approximately 0.99 and the uncertainty interval included 1.

For High stress compared with Low stress, the estimated odds ratio was approximately 0.16, with the interval remaining well below 1.

This pattern is consistent with the earlier multinomial analysis and suggests that the association between social support and stress is not adequately represented by one common effect across all stress levels.

The Bayesian model produced stable finite estimates despite the estimation problems observed in the categorical model.

This does not remove concerns about the unusual structure of the Social support variable or establish that the same pattern would occur in the wider student population.

## Overall interpretation

The analyses consistently show that greater study load is associated with higher stress.

Better sleep quality is generally associated with lower stress, although the relationship across individual score levels is not perfectly linear.

Social support requires more cautious interpretation.

Several analyses indicate that Social support behaves differently for Medium and High stress.

The unusual distribution of Social support across stress categories also limits how confidently this association can be generalized.

## Limitations

The dataset is observational, so causal conclusions cannot be made.

The complete wording and measurement details for some variables are not available in the data file.

Information about the sampling process is limited.

The sample should therefore not automatically be treated as representative of all university students.

Some associations in the dataset are unusually strong.

Several empty combinations occur between Social support and Stress level.

The proportional odds assumption is not equally convincing for all predictors.

Treating ordinal scores as numeric variables simplifies the relationships between their levels.

The Bayesian analysis improves estimation under difficult data patterns but does not solve possible problems related to measurement, sampling, or data construction.

## Repository structure

```text
academic stress research/
    README.md
    requirements.txt

    data/
        README.md
        StressLevelDataset.csv

    notebooks/
        analysis.ipynb

    report/
        mini_research_report.pdf

    figures/
        stress_by_study_load.png
        stress_by_sleep_quality.png
        stress_by_social_support.png
        predicted_stress_by_study_load.png
        predicted_stress_by_sleep_quality.png
        predicted_stress_by_social_support.png
```

## How to run

1. Create or activate a Python environment.
2. Install the packages:

```bash
pip install -r requirements.txt
```

3. Keep `StressLevelDataset.csv` inside the `data/` folder.
4. Open `notebooks/analysis.ipynb`.
5. Restart the kernel and run all cells from top to bottom.

The notebook saves the final figures automatically to `figures/`.
