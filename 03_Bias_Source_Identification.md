# Bias Source Identificatiom

## 1. Purpose

Bias in recommendation systems can emerge at any stage of the machine learning pipeline. This section provides a structured approach to identifying where bias originates and how it propagates through the system.

## 2. Sources of Bias Across the Pipeline
Data Collection Bias

Minority sellers have fewer interactions, producing sparse behavioural logs

Low-resource languages generate poor textual features

Low-bandwidth regions show incomplete session or impression data

Accessibility issues reduce data quality for users with assistive needs

Feature Engineering Bias

Features like price, delivery region, and past impressions encode socioeconomic patterns

Language-dependent features disproportionately penalise non-English content

Popularity-derived features disadvantage newcomers

Algorithmic Bias

Collaborative filtering favours high-activity users and sellers

Ranking models optimised for click-through favour clickbait or high-frequency items

Embeddings cluster minority sellers/items poorly due to sparse data

Feedback Loop Bias

Low exposure reduces future data, reinforcing the seller’s invisibility

Over-personalisation traps users in narrow content bubbles

High-spend users receive more exploration, further increasing skew

Deployment Bias

Promotion systems allocate traffic based on profitability rather than fairness

Explore/exploit mechanisms rarely sample long-tail sellers

Merchandising rules override ranking in ways that reduce fairness

## 3. Bias Traceability Table

Pipeline Stage: Data
Bias Type: Sampling bias
Example: Small sellers rarely appear in logs
Mitigation: Reweighting, fairness-aware sampling, additional exploration

Pipeline Stage: Model
Bias Type: Objective bias
Example: CTR-only optimisation
Mitigation: Multi-objective ranking including fairness terms

Pipeline Stage: Model
Bias Type: Embedding bias
Example: Poor embeddings for low-resource languages
Mitigation: Multilingual training, language-specific encoders

Pipeline Stage: Deployment
Bias Type: Exploration bias
Example: Popular items dominate explore slots
Mitigation: Fairness-adjusted explore/exploit policies

## 4. Output

The Bias Source Identification step results in a clear map of likely bias origins, linking observed disparities to specific pipeline components. This map guides mitigation planning and evaluation.
