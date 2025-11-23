# Historical Context Assessment (E-Commerce Personalisation)

## 1. Purpose

Personalisation systems have long been critiqued for amplifying structural inequities:

-Large sellers receive disproportionate visibility (“rich-get-richer feedback loops”).
-Underrepresented creators struggle to surface.
-Users with historically marginalised demographics receive fewer high-value opportunities (discounts, deals, visibility).
-Recommendation pipelines often rely on behavioural signals shaped by unequal access, digital literacy, socioeconomic status, and linguistic diversity.
-Understanding these patterns is the first step toward building fairer systems.

## 2. Structured Questionnaire
A. Domain & Application Context

What product/service does the recommendation system power?
Who are the users? (shoppers, creators, sellers)
What decisions does the model influence?
Who is most harmed by incorrect or unfair ranking?
What regulatory or platform policies apply? (EU AI Act, platform fairness commitments)

B. Historical Discrimination Patterns

Has the domain historically favoured certain sellers or content creators?
Are there known disparities in exposure between:
-Small vs large sellers?
-Newcomer vs established sellers?
-linguistic communities?
-user demographics?
Are there protected groups indirectly referenced through proxies (ZIP code, language, spending power)?

C. Intersectional Risks

Are certain groups doubly disadvantaged? e.g., small sellers in low-income regions, women-led businesses with low visibility, and users browsing in low-resource languages.
Does the platform support accessibility (screen readers, low-bandwidth users)? If not, who is excluded?

D. Mapping Historical Patterns onto ML Components
ML Component	Potential Historical Bias
Data logs	Underexposure of minority sellers → sparse signals
Feature engineering	Price, delivery region, past impressions → encode socioeconomic inequality
Objectives	: Click-through optimisation rewards popularity, not fairness
Sampling	Long-tail sellers rarely sampled → poor model performance
Deployment	Exploration budgets favour profitable segments
3. Risk Scoring Matrix
Historical Pattern	Severity	Likelihood	Relevance	Priority
“Rich-get-richer” exposure bias	3	3	3	9
Underrepresentation of regional languages	3	2	3	8
Intersectional disadvantage (women-led micro-businesses)	3	2	2	7
Bias toward premium/high-income segments	2	3	3	8
4. Output

A Historical Risk Profile summarising:

vulnerable seller/user segments

proxies likely to encode harm

fairness-sensitive features

deployment phases where harm is most likely to appear
