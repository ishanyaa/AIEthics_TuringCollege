# Fairness Metrics and Validation

## 1. Exposure Fairness Metrics (Seller-Side)

Normalised exposure ratios

Observed versus expected exposure

Relative exposure difference between seller groups

Gini coefficient of exposure distribution

## 2. User-Side Fairness Metrics

Equal opportunity: true positive rate parity across user groups

Calibration error across languages, regions, device types

Coverage parity: number of distinct items shown to each user segment

## 3. Individual Fairness Metrics

Recommendation overlap for users with similar embeddings

Counterfactual perturbation tests modifying proxy features (region, language)

## 4. Intersectional Fairness

Metrics should be evaluated across combinations such as:

Region × language

Gender × seller type

Socioeconomic segment × device type

Seller gender × region × product category

## 5. Statistical Validation and Robustness

95% confidence intervals for exposure gaps

Bootstrap tests for statistical significance

Sensitivity tests under noisy or partially missing data

Temporal robustness checks (daily or weekly fairness stability)

## 6. Validation Framework

Step 1: Compute baseline fairness metrics
Step 2: Identify disparities exceeding acceptable thresholds
Step 3: Apply mitigations (fairness-aware ranking, reweighting, improved embeddings)
Step 4: Recalculate metrics after mitigation
Step 5: Compare pre- and post-mitigation metrics using confidence intervals
Step 6: Produce final audit summary for stakeholders
