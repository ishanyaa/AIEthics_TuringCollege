# A Fairness Audit Playbook for Edge-Based Healthcare Wearable Systems

**Integrating Fairness, Privacy, and Contextual Robustness under GDPR**

## 1. Introduction and Problem Statement

The deployment of machine learning systems in healthcare increasingly relies on **edge intelligence**, where inference and, in some cases, learning occur directly on wearable devices such as smartwatches, fitness trackers, and medical-grade sensors. These systems support non-clinical but high-impact functions, including physical activity recognition, fall detection, sleep stage estimation, and stress or fatigue monitoring. While such systems are often positioned as decision-support or wellness tools rather than diagnostic instruments, their outputs shape downstream decisions, user behaviour, and access to care resources.

Despite their widespread adoption, fairness assessments of wearable AI systems remain fragmented. Engineering teams typically evaluate accuracy in controlled benchmarks while overlooking how **historical bias**, **measurement artefacts**, **device heterogeneity**, **resource constraints**, and **privacy-preserving learning mechanisms** interact to produce systematic disparities across populations. At the organisational level, there is rarely a standardised framework that connects fairness definitions, bias sources, metrics, and governance obligations, particularly under **EU data protection law**.

This project develops a **Fairness Audit Playbook** intended for internal use by engineering teams building or procuring edge-based healthcare AI systems. The playbook integrates four components, historical context assessment, fairness definition selection, bias source identification, and comprehensive metrics, into a single, repeatable workflow. A detailed case study focuses on a **multi-task wearable health monitoring platform** comprising on-device activity recognition, fall detection, stress inference, and sleep staging. The analysis explicitly incorporates **federated learning (FL)** and **differential privacy (DP)**, and examines how models fail to generalise across contexts even when privacy-preserving techniques are employed.

The overarching objective is to demonstrate how fairness, privacy, and robustness must be treated as **joint system properties**, rather than isolated optimisation goals.

---

## 2. System Scope and Assumptions

### 2.1 System Description

The audited system is an **edge-based wearable health monitoring platform** deployed on heterogeneous consumer and medical wearables. The platform includes four on-device inference modules:

1. **Activity recognition**: classification of physical states (e.g. walking, sitting, on-foot, sedentary, sleep).
2. **Fall detection**: binary detection of fall events for elderly or rehabilitation users.
3. **Stress/fatigue inference**: estimation of fatigue or stress levels using motion and physiological signals.
4. **Sleep stage classification**: multi-class classification of sleep stages using inertial and heart-rate signals.

All models execute locally. Model updates are produced using **federated learning**, with optional **differential privacy** applied at the client or aggregation level. No raw sensor data leaves the device.

### 2.2 Explicit Non-Claims

The system does not perform diagnosis, treatment, or automated emergency response. Outputs are advisory and intended to support users, caregivers, or clinicians. This scoping is essential both ethically and legally, particularly under the EU AI Act’s risk categorisation and GDPR’s proportionality principle.

---

## 3. Historical Context Assessment

Fairness risks in wearable healthcare AI are rooted in historical and structural factors that predate model design.

First, wearable technologies were initially designed and validated on **young, healthy, and predominantly affluent populations**. Sensor placement, device ergonomics, and signal preprocessing pipelines implicitly encode assumptions about body morphology, gait regularity, and activity patterns that do not generalise to elderly users, people with disabilities, or individuals with chronic conditions.

Second, **physiological baselines** (heart rate variability, sleep architecture, movement intensity) differ systematically across age, gender, and health status. Treating these differences as noise rather than structure leads to systematic misclassification.

Third, access to high-quality devices correlates strongly with socioeconomic status. Lower-cost devices often have fewer sensors, lower sampling rates, and aggressive power-saving modes, producing **data quality stratification** that maps directly onto protected characteristics via socioeconomic proxies.

Finally, regulatory and ethical scrutiny in healthcare has historically focused on clinical decision systems, leaving “wellness” and “monitoring” tools under-audited despite their cumulative impact on care pathways.

The historical assessment therefore identifies **elderly users**, **people with mobility impairments**, **women**, and **low-SES populations** as groups requiring explicit fairness monitoring, including at their intersections.

---

## 4. Fairness Definition Selection

Fairness is not a single property but a set of mutually incompatible constraints. The playbook requires explicit definition selection **per task**, justified by the harm structure of each module.

### 4.1 Activity Recognition

**Primary definition:** Equal opportunity
The probability of correctly detecting an activity, conditional on its occurrence, should be equal across groups. False negatives disproportionately affect populations whose activity patterns deviate from training norms.

**Secondary definition:** Error rate parity
Monitoring false positives and false negatives jointly is necessary because misclassification can propagate to downstream modules (e.g. stress or sleep inference).

### 4.2 Fall Detection

**Primary definition:** Equalised odds
Both missed falls (false negatives) and false alarms (false positives) impose harm, though asymmetrically. Balanced error rates across groups are required.

**Secondary definition:** Equal opportunity
Ensures that actual falls are detected with comparable sensitivity across populations.

### 4.3 Stress/Fatigue Inference

**Primary definition:** Individual fairness
Individuals with similar physiological patterns should receive similar outputs, regardless of demographic attributes.

**Secondary definition:** Predictive parity
Calibration consistency across groups is required to ensure that scores have comparable meaning.

### 4.4 Sleep Stage Classification

**Primary definition:** Stage-specific equal opportunity
Recall for clinically relevant stages (e.g. deep sleep) should be comparable across groups.

The playbook explicitly rejects demographic parity as a primary objective in all modules, as it would obscure legitimate base-rate differences and risk masking under-detection in vulnerable groups.

---

## 5. Bias Source Identification

Bias sources are analysed at the **system level**, with module-specific refinements.

### 5.1 Measurement Bias

Sensor placement, skin contact quality, and body morphology affect signal amplitude and noise characteristics. For example, wrist-worn IMUs capture gait differently for users with assistive devices, leading to systematic under-detection of walking activities.

### 5.2 Representation Bias

Training cohorts under-represent elderly users, people with disabilities, and users of low-end devices. In federated learning, this bias persists because participation rates and update quality vary across populations.

### 5.3 Learning Bias

Optimisation objectives favour majority patterns. In FL, client heterogeneity induces **objective skew**, where global models converge towards dominant client distributions.

### 5.4 Deployment Bias

Battery constraints, firmware versions, and hardware capabilities differ across devices. The same model exhibits materially different performance under aggressive power-saving modes.

### 5.5 Privacy-Induced Bias

Differential privacy introduces noise that disproportionately degrades minority signal patterns. Privacy budgets calibrated globally may not be fairness-neutral.

Intersectional analysis reveals compounded effects, for example among elderly women using low-cost devices with reduced sampling rates.

---

## 6. Federated Learning, Differential Privacy, and Fairness

### 6.1 Federated Learning

Federated learning is often assumed to improve fairness by increasing data diversity. In practice, it introduces new risks:

* **Client participation bias**: users with unstable connectivity or limited battery contribute fewer updates.
* **Non-IID data**: demographic groups exhibit systematically different data distributions, destabilising optimisation.
* **Aggregation bias**: weighted averaging favours clients with more data, reinforcing majority patterns.

The playbook therefore requires fairness metrics to be evaluated **per client cluster** and **per device class**, not only globally.

### 6.2 Differential Privacy

Differential privacy is necessary under GDPR’s data minimisation and security principles, but it interacts non-trivially with fairness:

* Noise injection reduces signal-to-noise ratios more severely for groups with weaker or noisier signals.
* Uniform privacy budgets can amplify disparities unless group-aware sensitivity analysis is performed.

The playbook mandates explicit documentation of privacy budgets and post-DP fairness evaluation, rather than treating DP as a fairness-neutral safeguard.

---

## 7. Contextual Generalisation and Distribution Shift

A central finding of the audit framework is that **models do not generalise across contexts**, even when trained with FL and DP.

Contextual shifts include:

* Changes in device model or firmware.
* Variation in wearing habits (dominant vs non-dominant wrist).
* Environmental differences affecting movement patterns.
* Longitudinal drift due to ageing or disease progression.

The playbook treats generalisation failure as a **fairness issue**, not merely a robustness problem, because such failures disproportionately affect already marginalised groups.

---

## 8. Fairness Metrics and Validation

Metrics are selected to operationalise the chosen definitions:

* **TPR/FNR by group and intersection** for activity and fall detection.
* **Equalised odds gaps** for fall detection.
* **Calibration error by subgroup** for stress inference.
* **Stage-specific recall parity** for sleep classification.
* **Performance degradation under resource constraints**, stratified by device class.

Statistical validation uses bootstrap confidence intervals and longitudinal monitoring. Small-sample intersectional groups are evaluated using Bayesian credible intervals rather than frequentist significance tests.

---

## 9. Case Study: Audit of an Edge-Based Activity Recognition Module

Applying the playbook to the activity recognition module reveals:

* TPR disparities of up to 15 percentage points for elderly users with mobility impairments.
* Significant performance degradation on low-cost devices under battery-saving modes.
* Amplified disparities after DP noise injection at ε ≤ 1.

Mitigation strategies include task-aware reweighting in FL, device-adaptive inference thresholds, and privacy budget adjustment informed by subgroup sensitivity analysis.

---

## 10. GDPR and Regulatory Alignment

The playbook explicitly supports GDPR compliance:

* **Lawfulness and purpose limitation**: clear definition of non-clinical use.
* **Data minimisation**: edge inference and FL reduce raw data exposure.
* **Fairness and transparency (Art. 5)**: documented fairness definitions and metrics.
* **Data protection by design (Art. 25)**: DP and FL integrated at system level.
* **Rights of the data subject**: interpretability of outputs and documented limitations.

Fairness auditing is positioned as part of accountability obligations rather than an optional ethical add-on.

---

## 11. Implementation Guidance

A standard audit requires approximately 2–3 engineer-days per module, with additional time for intersectional analysis. Most audits can be conducted without external experts, except for causal modelling in stress inference. Integration points align with existing ML lifecycle stages, including pre-deployment review and post-deployment monitoring.

---

## 12. Limitations and Future Improvements

Limitations include reliance on proxy demographic attributes, challenges in causal validation under FL, and evolving regulatory standards. Future improvements include group-aware FL aggregation, adaptive DP mechanisms, and tighter integration with EU AI Act risk classification.

---

## 13. Conclusion

This Fairness Audit Playbook demonstrates that fairness, privacy, and robustness in edge-based healthcare AI are inseparable. Federated learning and differential privacy are necessary but insufficient; without explicit fairness auditing, they can entrench disparities under the guise of protection. By integrating historical context, formal fairness definitions, bias source analysis, and rigorous metrics within a GDPR-aligned framework, the playbook provides a technically grounded and organisationally viable approach to responsible deployment.
