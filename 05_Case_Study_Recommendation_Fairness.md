# Case Study: E-Commerce Personalised Recommendations

## 1. System Overview

The platform serves a large user base with diverse linguistic and regional backgrounds. The recommendation system powers the home feed, search ranking, and promotional placements. Concerns were raised that:

Small sellers were losing visibility

Regional-language users were receiving lower-quality recommendations

New sellers were not surfacing in personalised feeds

A full fairness audit was requested to quantify these issues and propose targeted mitigations.

## 2. Historical Context Summary

Key risks identified:

Strong popularity bias favouring already-successful sellers

Underrepresentation of sellers who publish listings in regional languages

Lower interaction data quality for low-income or low-bandwidth user segments

Intersectional disadvantage for women-led micro-businesses in competitive categories

##  3. Selected Fairness Definitions

Primary metrics:

Exposure fairness

Equal opportunity across user groups

Calibration for language and region groups

Secondary metrics:

Diversity and coverage

Demographic parity as a monitoring signal

## 4. Bias Identification Findings
Data-Related

Minority and newcomer sellers had sparse impressions

Product descriptions in non-English languages produced weaker embeddings

User activity patterns varied significantly by device type and bandwidth

Model-Related

Ranking was optimised mainly for click-through

Collaborative filtering reinforced high-activity clusters

Embeddings failed to represent regional-language listings accurately

Deployment-Related

Promotional modules prioritised high-conversion sellers

Explore slots were concentrated in premium categories

## 5. Baseline Fairness Metrics

Seller-side exposure ratios:

Small sellers: 0.42 (relative to expected)

Regional-language sellers: 0.38

Women-led micro-businesses: 0.45

User-side gaps:

True positive rate gap between English and Hindi users: 12%

Calibration error for regional users: 3.8 times higher than the majority group

Intersectional gaps:

Regional-language small sellers: 71% exposure shortfall

## 6. Mitigation Interventions

Introduced fairness-aware ranking with multi-objective optimisation

Increased exploration budget for long-tail sellers

Improved multilingual embeddings using domain-relevant corpora

Adjusted sampling to include underrepresented sellers more frequently

Deployed minimum exposure guarantees for critical seller categories

## 7. Post-Mitigation Outcomes

Seller-side improvements:

Small sellers: 0.42 to 0.78

Regional-language sellers: 0.38 to 0.73

Intersectional group: 0.29 to 0.66

User-side improvements:

TPR gap reduced from 12% to 3.5%

Calibration error normalised across language groups

Recommendation diversity increased by 18%

Statistical tests confirmed that improvements were significant.

## 8. Key Insights

Popularity-driven objectives were the largest contributor to unfair exposure

Multilingual and low-resource data weaknesses substantially affected model fairness

Intersectional fairness analysis revealed disparities hidden at the group level

Business metrics remained stable after fairness improvements

## 9. Recommendations for Ongoing Monitoring

Continuous fairness dashboards

Regular recalculation of exposure and calibration metrics

Quarterly audits following major model updates

Incorporation of fairness constraints in retraining pipelines
