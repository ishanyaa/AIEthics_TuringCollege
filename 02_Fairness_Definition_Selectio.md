# Fairness Definition Selection

## 1. Purpose

Fairness definitions capture the values a recommendation system aims to uphold. In e-commerce, fairness applies to both users (who receive equitable recommendations) and sellers (who receive equitable exposure). This component helps teams select appropriate fairness definitions based on historical risks, business goals, and technical feasibility.

## 2. Relevant Fairness Definitions for Recommendation Systems
Exposure Fairness (Seller-Side)

Ensures that groups of items or sellers receive exposure proportional to their relevance or demand. This helps counter popularity-driven imbalance.

Equal Opportunity (User-Side)

Users with similar intent should receive comparable-quality recommendations regardless of language, region, or demographic segment.
Formally: equal true positive rates across groups for engagement labels (e.g., clicks or add-to-cart).

Calibration

Recommendation scores should reflect the true likelihood of engagement across all user groups. A predicted engagement score should have the same meaning across all user segments.

Demographic Parity (Monitoring Only)

Checks whether the distribution of recommendations is disproportionately skewed toward or away from specific groups. Often used as a secondary metric due to strong utility trade-offs.

Individual Fairness

Users with similar behavioural profiles should receive similar recommendation sets. Evaluated through embedding similarity or neighbourhood-based comparisons.

## 3. Decision Workflow

Identify who the fairness obligations apply to:

Sellers: exposure fairness

Users: equal opportunity and calibration

Both: multi-stakeholder fairness

Determine the most harmful errors:

Underexposure of small or minority sellers → exposure fairness

Poor-quality recommendations for certain user segments → equal opportunity

Systematic misalignment across languages or regions → calibration

Consider utility constraints:

Strict demographic parity may conflict with personalisation objectives

Use it primarily as a monitoring metric

Account for multilingual and socioeconomic diversity:

Add calibration and equal opportunity checks across language and region groups

Include intersectional combinations wherever feasible

## 4. Final Selection for E-Commerce Case Study

Primary fairness definitions:

Exposure fairness

User equal opportunity

Calibration across language and region groups

Secondary metrics:

Demographic parity of recommendation distribution

Coverage and diversity metrics
