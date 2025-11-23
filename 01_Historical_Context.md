# Historical Context Assessment (E-Commerce Personalisation)

## 1. Purpose

Personalised recommendation systems in e-commerce have historically reinforced structural inequities. Several patterns consistently appear across platforms:
Large or well-established sellers gain disproportionate visibility, creating “rich-get-richer” exposure loops.
Underrepresented or niche creators struggle to surface in recommendations.
Users from marginalised demographics often receive fewer high-value opportunities such as discounts or personalised promotions.
Behavioural signals used for ranking frequently reflect unequal access, digital literacy gaps, socioeconomic divides, and linguistic constraints.
Identifying these historical patterns is crucial for designing a more equitable recommendation pipeline. This assessment sets the foundation for later fairness definition selection, bias tracing, and metric evaluation.

## 2. Structured Questionnaire

A. Domain & Application Context
What product or service does the recommendation system support?
Who are the primary users (shoppers, creators, sellers)?
What decisions does the model influence (ranking, search suggestions, promotions, discount allocation)?
Who is most harmed when recommendations are incorrect or unfair?
What regulatory or platform-level policies apply (EU AI Act, marketplace fairness policies, accessibility standards)?

B. Historical Discrimination Patterns
Has the platform historically favoured certain seller segments (large brands, premium sellers, early adopters)?
Are there known disparities in exposure across:
small vs large sellers
newcomer vs established sellers
linguistic communities
demographic groups
Are protected groups indirectly referenced through proxy features such as:
region or ZIP code
language metadata
device type
spending power or purchase history

C. Intersectional Risks

Are any groups facing compounded disadvantages, such as:
small sellers in low-income regions
women-led micro-businesses
sellers producing content in low-resource languages
Does the platform support accessibility needs such as screen readers, low-bandwidth usage, and alternative input modes?
If not, which segments are excluded?

D. Mapping Historical Patterns onto ML Components

Data logs: Underexposure of minority sellers leading to weak or sparse learning signals
Feature engineering: Variables such as price, delivery region, and impressions may encode socioeconomic inequality
Objectives: Click-through–focused optimisation tends to reward popularity rather than fairness
Sampling: Long-tail sellers are rarely sampled during training, reducing model generalisation
Deployment: Exploration budgets often prioritise profitable or popular segments

3. Risk Scoring Matrix

Historical Pattern: “Rich-get-richer” exposure bias
Severity: 3
Likelihood: 3
Relevance: 3
Priority: 9

Historical Pattern: Underrepresentation of regional languages
Severity: 3
Likelihood: 2
Relevance: 3
Priority: 8

Historical Pattern: Intersectional disadvantage (women-led micro-businesses)
Severity: 3
Likelihood: 2
Relevance: 2
Priority: 7

Historical Pattern: Bias toward premium or high-income market segments
Severity: 2
Likelihood: 3
Relevance: 3
Priority: 8

4. Output

The Historical Context Assessment delivers a clear Historical Risk Profile summarising:

Seller and user groups most vulnerable to unfair recommendations
Proxy variables likely to encode demographic or socioeconomic disadvantage
Features and model components that require special attention
Deployment phases where unfair exposure patterns are most likely to appear
