# AI in Employment: Fairness Audit Report

**Course**: MAIB AI 219 – Ethics, Sociology, and Governance of AI
**Case Framing**: AI in Employment (HireVue-style screening risks)
**Date**: January 2026

---

## Executive Summary

This report presents a comprehensive fairness audit of AI-driven employment screening systems, using the **FairJob dataset** (Criteo, HuggingFace) as a proxy for HireVue-style algorithmic hiring tools. Our analysis reveals measurable disparities between protected groups, with the unprivileged group experiencing **8.5% lower positive outcome rates**. While overall metrics pass the legal 4/5ths rule threshold, intersectional analysis reveals concerning disparities in non-senior positions. Two mitigatiåon strategies—**threshold adjustment** and **combined reweighing**—successfully achieved near-perfect statistical parity while maintaining acceptable model performance.

---

## Section A: Dataset Selection and Justification

### Dataset Used: FairJob (HuggingFace: criteo/FairJob)

**Why FairJob was selected:**
1. **Direct relevance**: FairJob is specifically designed for fairness research in job recommendation systems, closely mirroring HireVue's screening function where algorithms determine which candidates receive favorable exposure.

2. **Scale**: 1,072,226 records provide statistically robust analysis, unlike smaller synthetic alternatives.

3. **Real-world provenance**: Based on actual job recommendation data with anonymized protected attributes, avoiding the limitations of fully synthetic data.

4. **Alignment with HireVue case**: Both systems operate as **gatekeepers** determining which candidates advance:
   - HireVue: Determines which candidates reach human review
   - FairJob: Determines which job recommendations receive engagement (positive exposure)

**Dataset Characteristics:**

| Attribute | Value |
|-----------|-------|
| Total Records | 1,072,226 |
| Features | 56 (13 categorical, 35 numerical, 8 contextual) |
| Missing Values | 0 (clean dataset) |
| Protected Groups | 2 (binary, evenly split: 536,113 each) |
| Target Variable | `click` (binary: job engagement) |
| Positive Rate | 0.70% (class imbalanced) |

**Key Limitation**: The protected attribute is anonymized (likely gender), preventing explicit demographic labeling. We use "Group A" (privileged) and "Group B" (unprivileged) based on observed outcome rates.

---

## Section B: Key Bias Findings (Top 5 Bullets)

### 1. **Overall Disparate Impact: 8.5% Disadvantage for Group B**
- Group A selection rate: **0.729%**
- Group B selection rate: **0.668%**
- Disparate Impact Ratio (DIR): **0.9153**
- Passes 4/5ths rule (≥0.80) but represents meaningful disparity at scale

### 2. **Intersectional Amplification in Non-Senior Positions**
- Non-senior jobs: DIR = **0.8228** (near legal threshold)
- Senior jobs: DIR = **0.9443** (better parity)
- Bias is **17% worse** for entry-level positions—exactly where equal opportunity matters most

### 3. **Model Predictions Perpetuate Historical Bias**
- Logistic Regression baseline: DIR = **0.9285**, SPD = **-2.29 pp**
- Decision Tree baseline: DIR = **0.9690**, SPD = **-0.96 pp**
- Without mitigation, models learn and reproduce historical disparities

### 4. **Exposure Patterns Show Subtle Position Bias**
- Top 5 rank positions: Group A 54.80% vs Group B 54.25%
- Click rate at top positions: Group A **1.01%** vs Group B **0.98%**
- Same exposure → different outcomes suggests recommendation quality differences

### 5. **Mitigation Achieves Near-Perfect Parity**
- Threshold Adjustment: DIR = **1.0003** (perfect parity), SPD = **0.01 pp**
- Combined Reweighing: DIR = **1.0103**, with improved F1 score
- Fairness is achievable without catastrophic accuracy loss

---

## Section C: Ethics Lens Analysis

### Consequentialist Perspective (Utilitarian/Outcomes-Based)

**Harms Identified:**

| Stakeholder | Harm | Magnitude |
|-------------|------|-----------|
| Group B candidates | Reduced job exposure and opportunities | 8.5% fewer positive outcomes |
| Non-senior applicants | Amplified bias at career entry | 17.7% worse DIR vs. senior |
| Labor market | Talent misallocation | Qualified candidates filtered out |
| Employers | Suboptimal hiring | Missing diverse candidates |

**Utilitarian Calculus:**
- **Without mitigation**: System generates profit for platform while distributing harm to unprivileged group—violates "greatest good for greatest number"
- **With mitigation**: Threshold adjustment achieves parity with minimal accuracy loss (70.3% vs 69.3%), demonstrating that fairness and efficiency are not mutually exclusive
- **Key insight**: The "efficiency" argument for biased systems fails when mitigation is technically feasible

### Deontological Perspective (Rights-Based/Kantian)

**Fundamental Rights Violated:**

1. **Right to Equal Consideration**: Candidates deserve evaluation based on qualifications, not group membership. A DIR of 0.8228 in non-senior positions means 1 in 5 Group B candidates who would receive a positive outcome under equal treatment are denied.

2. **Right to Transparency**: The FairJob dataset (like HireVue) uses anonymized features—candidates cannot understand why they were rejected. This violates the Kantian principle that persons should never be treated merely as means (data points) but as ends (autonomous agents deserving explanation).

3. **Procedural Fairness**: Even if outcomes appear statistically fair at aggregate level, the process of using opaque ML features (num16, num27, etc.) to determine employment opportunities treats humans as objects of prediction rather than subjects of deliberation.

**Categorical Imperative Test:**
- "If every employer used biased screening systems, would this be universally acceptable?"
- Answer: No. Universal adoption would systematically exclude protected groups from economic participation—a maxim that contradicts itself by destroying the labor market it depends upon.

### Virtue Ethics Perspective (Character/Organizational Values)

**Organizational Virtues at Stake:**

| Virtue | Assessment | Evidence |
|--------|------------|----------|
| **Justice** | Compromised | 8.5% disparity without active mitigation |
| **Transparency** | Failing | Feature importance shows num27 (0.34) and rank (0.26) drive decisions—neither interpretable |
| **Prudence** | Partial | Class weighting shows awareness of imbalance, but intersectional effects ignored |
| **Accountability** | Absent | No mechanism for candidates to challenge algorithmic decisions |

**Virtue Ethics Prescription:**
Organizations deploying hiring AI should ask: "What kind of employer do we want to be?" A virtuous organization would:
1. Conduct pre-deployment bias audits (demonstrated in this report)
2. Implement mitigation before launch (threshold adjustment is immediately deployable)
3. Create appeals processes for algorithmic rejections
4. Publicly report fairness metrics annually

---

## Section D: Sociology Lens Analysis

### Power Asymmetry

**Information Asymmetry Structure:**

```
Employers/Platforms          →    Complete visibility into candidate data
        ↓                         Feature engineering, model selection
AI Vendor (HireVue/Criteo)   →    Proprietary algorithm, training data
        ↓                         Audit results often undisclosed
Candidates (Job Seekers)     →    No visibility into decision factors
                                  No explanation for rejection
                                  No appeals process
```

**Power Concentration:**
- Platforms aggregate data from millions of applications, creating **winner-take-all dynamics**
- Individual candidates cannot opt out—algorithmic screening is industry standard
- Collective action (unionization, regulation) is the only countervailing force

### Who Benefits vs. Who is Harmed

| Beneficiary | Mechanism | Magnitude |
|-------------|-----------|-----------|
| Platform vendors | Per-candidate licensing fees | Revenue regardless of fairness |
| Employers | Reduced HR costs | ~70% screening automation |
| Group A candidates | Historical advantage encoded | 8.5% better outcomes |

| Harmed Party | Mechanism | Magnitude |
|--------------|-----------|-----------|
| Group B candidates | Lower recommendation rates | 8.5% fewer opportunities |
| Non-senior applicants | Entry-level bias amplification | 17.7% worse DIR |
| Candidates with disabilities | Modal assumptions (HireVue: speech/video) | Systematic exclusion |

### Opacity and Algorithmic Blackballing

**Opacity Mechanisms in FairJob:**
- 35 numerical features (num16-num50) with no semantic meaning
- Candidates cannot know which behaviors to modify
- Creates **learned helplessness**—rejection without explanation prevents adaptation

**Blackballing Risk:**
- Negative assessments may persist across applications
- If employers share ATS data, one algorithmic rejection compounds into permanent exclusion
- Particularly acute for Group B: initial bias → rejection → worse training data → amplified future bias

---

## Section E: Governance Lens Analysis

### Title VII Disparate Impact and 4/5ths Rule

**Legal Framework:**
Under Title VII of the Civil Rights Act (1964), employment practices with disparate impact on protected groups are unlawful unless justified by business necessity and no less discriminatory alternative exists.

**EEOC Four-Fifths Rule Application:**

| Metric | Group A | Group B | DIR | 4/5ths Compliance |
|--------|---------|---------|-----|-------------------|
| Overall Selection Rate | 0.729% | 0.668% | 0.9153 | **PASS** (≥0.80) |
| Non-Senior Positions | 0.666% | 0.548% | 0.8228 | **PASS** (marginal) |
| Model Predictions (LR) | 32.09% | 29.80% | 0.9285 | **PASS** |

**Key Legal Findings:**
1. **Overall compliance**: The system passes the 4/5ths rule, but this does not eliminate liability
2. **Intersectional scrutiny**: Non-senior positions at 0.8228 DIR warrant deeper investigation
3. **Less discriminatory alternatives exist**: Threshold adjustment achieves DIR = 1.0003—EEOC guidance requires adoption
4. **Vendor liability**: Per *Mobley v. Workday* (2023-2025), employers cannot delegate discrimination to AI vendors

### ADA Accommodation Implications

**HireVue-Specific Context (ACLU v. Intuit/HireVue, March 2025):**
- Video-based assessment disadvantages deaf, blind, and neurodiverse candidates
- Speech pattern analysis penalizes non-native speakers and those with speech differences
- FairJob's numerical features may similarly encode disability proxies (e.g., response timing, interaction patterns)

**Required Accommodations:**
1. **Pre-assessment disclosure**: Inform candidates how AI evaluates them
2. **Alternative modalities**: Non-video options for accessibility
3. **Human override**: Accommodation requests must bypass algorithmic filtering
4. **Post-hoc review**: Disability-related rejections require human verification

### EU AI Act: High-Risk Classification

**Regulatory Status:**
Under the EU AI Act (effective August 2026-2027), employment AI systems are classified as **HIGH-RISK**, requiring:

| Requirement | FairJob/HireVue Assessment |
|-------------|---------------------------|
| Risk assessment & mitigation | This report demonstrates feasibility |
| High-quality training data | Protected attribute balance achieved |
| Activity logging | Requires implementation |
| Detailed documentation | Feature semantics needed |
| Human oversight | Not currently enforced |
| Robustness & cybersecurity | Not assessed |

**Compliance Gap:**
- Current systems (FairJob proxy) lack explainability—num27's 34% importance is meaningless to regulators
- Human oversight is nominal—80% of HireVue users automate filtering
- Documentation requirements will force feature transparency

---

## Section F: Practical Recommendations

### Technical Recommendations

1. **Mandatory Pre-Deployment Bias Audit**
   - Compute DIR, SPD, and intersectional metrics before launch
   - Threshold: DIR ≥ 0.90 for deployment (stricter than legal 4/5ths)
   - Re-audit quarterly with production data

2. **Implement Threshold Adjustment**
   - Demonstrated to achieve DIR = 1.0003 with minimal accuracy loss
   - Group-specific thresholds: Group A = 0.515, Group B = 0.499
   - Requires protected attribute at inference (may need proxy methods)

3. **Feature Transparency Protocol**
   - Replace opaque numerical features with interpretable signals
   - Document relationship between features and business outcomes
   - Remove features correlated with protected attributes (proxy discrimination)

4. **Continuous Monitoring Dashboard**
   - Real-time tracking of selection rates by group
   - Automated alerts when DIR drops below 0.85
   - Monthly intersectional reports (group × seniority × role)

### Organizational Recommendations

1. **Human-in-the-Loop Requirements**
   - All algorithmic rejections reviewed by trained HR staff
   - Reviewers empowered to override algorithmic recommendations
   - Document override rates by demographic (detect rubber-stamping)

2. **Candidate Appeals Process**
   - Structured mechanism for candidates to request review
   - Time-bound response requirements (e.g., 5 business days)
   - Feedback on rejection reasons (within legal bounds)

3. **Vendor Accountability**
   - Contractual requirements for bias audits
   - Access to fairness metrics as condition of procurement
   - Liability sharing for disparate impact violations

4. **Training and Awareness**
   - HR staff training on algorithmic bias
   - Leadership briefings on legal exposure
   - Annual fairness certification for hiring managers

### Policy-Level Recommendations

1. **Documentation Requirements**
   - Model cards specifying intended use, known limitations, and bias metrics
   - Data sheets documenting training data demographics and collection methods
   - Update requirements when model or data changes

2. **Algorithmic Impact Assessments**
   - Pre-deployment assessment of fairness, privacy, and societal impact
   - Public disclosure of aggregate fairness metrics
   - Third-party audit requirement for high-volume systems

3. **Accountability Mechanisms**
   - Designated "Algorithmic Accountability Officer" role
   - Board-level reporting on AI fairness metrics
   - Whistleblower protections for employees identifying bias

---

## Appendix: Technical Details

### Fairness Metrics Definitions

| Metric | Formula | Interpretation |
|--------|---------|----------------|
| Disparate Impact Ratio (DIR) | P(Y=1\|unprivileged) / P(Y=1\|privileged) | ≥0.80 per EEOC |
| Statistical Parity Difference (SPD) | P(Y=1\|unprivileged) - P(Y=1\|privileged) | 0 = parity |
| Equal Opportunity Difference (EOD) | TPR_unprivileged - TPR_privileged | 0 = equal TPR |

### Model Performance Summary

| Model | Accuracy | F1 | ROC-AUC | DIR | Passes 4/5ths |
|-------|----------|-----|---------|-----|---------------|
| Logistic Regression (Baseline) | 69.3% | 2.8% | 76.9% | 0.929 | YES |
| Decision Tree (Baseline) | 69.7% | 3.1% | 75.9% | 0.969 | YES |
| Combined Reweighing | 95.1% | 5.9% | 76.5% | 1.010 | YES |
| Threshold Adjustment | 70.3% | 2.9% | 76.9% | 1.000 | YES |

### Files Generated

| File | Description |
|------|-------------|
| `outputs/tables/cleaned_dataset.csv` | 100k sample of cleaned data |
| `outputs/tables/dataset_summary.csv` | Dataset statistics |
| `outputs/tables/selection_rates_by_group.csv` | Group-wise selection rates |
| `outputs/tables/fairness_metrics_pre_mitigation.csv` | Pre-mitigation metrics |
| `outputs/tables/intersectional_analysis.csv` | Group × seniority analysis |
| `outputs/tables/exposure_analysis.csv` | Rank-based exposure metrics |
| `outputs/tables/model_comparison_baseline.csv` | Baseline model comparison |
| `outputs/tables/final_mitigation_comparison.csv` | Mitigation results |
| `outputs/figures/mitigation_comparison.png` | Visual comparison of approaches |
| `outputs/figures/fairness_accuracy_tradeoff.png` | Tradeoff analysis |
| `outputs/figures/intersectional_bias_analysis.png` | Intersectional visualization |

---

## Conclusion

This audit demonstrates that AI employment screening systems—proxied by the FairJob dataset—exhibit measurable bias against unprivileged groups, with particular severity in entry-level positions where opportunity equity matters most. While aggregate metrics may satisfy legal thresholds, this represents a minimum standard, not an ethical aspiration.

The technical feasibility of mitigation (threshold adjustment achieving near-perfect parity) shifts the ethical burden: organizations can no longer claim ignorance or impossibility. The choice to deploy unmitigated systems is now a choice to discriminate.

From ethical, sociological, and governance perspectives, the path forward is clear:
1. **Audit before deployment** (this report provides a template)
2. **Mitigate with proven techniques** (threshold adjustment, reweighing)
3. **Monitor continuously** (fairness metrics as KPIs)
4. **Ensure human oversight** (appeals, overrides, accountability)

The question is not whether fair AI hiring is possible—it is. The question is whether organizations will choose to implement it.

---

*Report prepared for MAIB AI 219: Ethics, Sociology, and Governance of Artificial Intelligence*
*Analysis conducted using FairJob dataset (criteo/FairJob) from HuggingFace*
