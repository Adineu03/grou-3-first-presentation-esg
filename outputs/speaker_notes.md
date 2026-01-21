# Speaker Notes: AI in Employment

**Total Time:** 8–10 minutes
**Pace:** ~45–50 seconds per slide

---

## Slide 1 — Title
**[0:00–0:20]**

> "Good morning/afternoon. We're Group 3, and today we're presenting on AI in Employment—specifically examining the ethics, sociology, and governance implications of algorithmic hiring systems."

- Pause briefly to let the title register
- Make eye contact with the audience
- No need to read the slide—it speaks for itself

**Transition:** "Let's start with why this matters."

---

## Slide 2 — Why AI in Employment Matters
**[0:20–1:10]**

> "Automated screening tools are now embedded across hiring pipelines—from resume filters to video interview scoring. But here's the critical framing: these systems don't just assist hiring decisions. They act as gatekeepers."

**Key points to hit:**
- Emphasize "gatekeepers"—this is the conceptual anchor for the whole talk
- "Upstream exclusion" means candidates are filtered out before any human sees them
- The bias doesn't need to be large—at scale, small disparities affect thousands

> "The core problem is simple: if you're filtered out by an algorithm, you never reach the hiring manager. You never get a chance to explain yourself. You never even know why."

**Transition:** "So what exactly do these systems do?"

---

## Slide 3 — System Framing
**[1:10–2:00]**

> "Hiring AI systems rank candidates by predicted 'fit'—but fit to what? Usually to historical patterns of who was hired before. HireVue-style systems go further: they analyze video interviews, speech patterns, even facial expressions."

**Key points to hit:**
- HireVue is a real company—700+ enterprise clients, millions of candidates screened
- EU AI Act explicitly classifies employment AI as "high-risk"
- Explain FairJob briefly: "We used FairJob—a real dataset of over one million job recommendations—as a proxy to study these dynamics empirically."

> "FairJob mirrors what HireVue does: it determines who gets recommended, who gets visibility, who gets a shot."

**Transition:** "Let me walk you through our audit approach."

---

## Slide 4 — Dataset & Audit Approach
**[2:00–2:45]**

> "FairJob contains over one million job recommendation records with two protected groups—anonymized, but evenly split. The target variable is job engagement: did the candidate click on the recommended job? Think of this as a proxy for 'did the system give you a fair shot?'"

**Key points to hit:**
- 1.07 million records—statistically robust
- 0.70% positive rate—highly imbalanced, typical of recommendation systems
- Our focus was explainability, not prediction accuracy

> "We approached this as an audit, not a modeling competition. The question wasn't 'how accurate can we get?' It was 'is this system fair?'"

**Transition:** "And here's what we found."

---

## Slide 5 — Initial Bias Findings
**[2:45–3:40]**

> "At first glance, the system looks compliant. Overall Disparate Impact Ratio is 0.91—above the legal threshold of 0.80. But look closer."

**Point to the table:**
- Overall DIR: 0.915 — passes
- Non-senior DIR: 0.823 — barely passes, marginal
- Group B has an 8.5% systematic disadvantage

> "The disparity is worse for entry-level positions—exactly where equal opportunity matters most. If you're just starting your career and you're in Group B, you're already behind."

**Explain metrics briefly:**
> "DIR is the ratio of positive outcomes between groups—0.80 is the legal floor. SPD is the raw difference—zero means parity."

**Transition:** "But here's the deeper problem..."

---

## Slide 6 — Why Aggregate Fairness Misleads
**[3:40–4:30]**

> "Aggregate metrics can hide localized harm. The system 'passes' overall, but non-senior positions show 17% worse disparity than senior roles."

**Point to the chart:**
- Left chart: Selection rates by group and seniority
- Right chart: DIR by seniority level—non-senior is visibly lower

> "This is the intersectional insight: if you only look at the average, you miss where the harm concentrates. Legal compliance is a floor, not a ceiling."

**Quote to emphasize:**
> "Intersectional analysis reveals what aggregate metrics obscure."

**Transition:** "Now let's apply our ethical frameworks."

---

## Slide 7 — Ethics Lens
**[4:30–5:20]**

> "We analyzed this through three ethical lenses."

**Walk through each card:**

1. **Consequentialism:** "8.5% disadvantage translates to real harm—thousands of lost opportunities. And since mitigation is feasible, choosing not to act is choosing to maximize harm."

2. **Deontology:** "Candidates have a right to equal consideration. When opaque features determine your fate and you never get an explanation, you're being treated as a data point, not a person."

3. **Virtue Ethics:** "What kind of organization deploys biased screening? Justice, transparency, and accountability are compromised when efficiency becomes the only value."

**Transition:** "The sociology lens adds another layer."

---

## Slide 8 — Sociology Lens
**[5:20–6:10]**

> "From a sociological perspective, we see algorithmic gatekeeping—AI decides who is seen, replacing human judgment with pattern matching."

**Key points:**
- **Power asymmetry:** Platforms see everything; candidates see nothing
- **Opacity creates helplessness:** If you don't know why you were rejected, you can't improve

**Point to the boxes:**
> "Who benefits? Platforms, employers, and historically privileged groups. Who's harmed? Unprivileged groups, entry-level applicants, and people with disabilities whose communication styles don't fit the model."

**Transition:** "This brings us to governance."

---

## Slide 9 — Governance Lens
**[6:10–7:00]**

> "Three regulatory frameworks matter here."

**Walk through each:**

1. **Title VII:** "Disparate impact doctrine applies to AI. The 4/5ths rule sets the floor. And crucially—employers are liable even for vendor algorithms. You can't outsource discrimination."

2. **ADA:** "HireVue's video analysis disadvantages deaf and disabled applicants. The ACLU filed a complaint in March 2025. Accommodations must be provided before assessment, not after."

3. **EU AI Act:** "Employment AI is classified as high-risk. That means mandatory bias audits, documentation, human oversight, and activity logging—effective 2026-2027."

**Key quote:**
> "Compliance is a minimum standard—it is not ethical adequacy."

**Transition:** "But here's the good news."

---

## Slide 10 — Mitigation Is Feasible
**[7:00–7:50]**

> "We tested two mitigation strategies, and both work."

**Point to the chart:**
- **Reweighing:** Adjust sample weights to correct historical bias → DIR improves to 1.01
- **Threshold adjustment:** Use group-specific thresholds → DIR reaches 1.00, perfect parity

> "And critically—there's no major performance loss. ROC-AUC stays at 77%. This isn't a tradeoff between fairness and accuracy. It's just a choice."

**Point to the metric cards:**
> "Baseline DIR was 0.93. After mitigation: 1.00. The gap closes completely."

**Transition:** "Which brings us to the key implication."

---

## Slide 11 — The Accountability Shift
**[7:50–8:40]**

> "Once mitigation is technically feasible—and we've shown it is—inaction becomes a choice."

**Pause for emphasis.**

> "Organizations can no longer claim ignorance or impossibility. The ethical burden shifts. If you can fix it and you don't, that's a decision."

**Key points:**
- "Can" implies "must"—capability creates obligation
- The question isn't whether fair AI hiring is possible. It is. The question is whether organizations will choose to implement it.

**Transition:** "Let me leave you with our conclusions."

---

## Slide 12 — Conclusions
**[8:40–9:30]**

> "Four takeaways."

**Read each bullet with conviction:**

1. "AI hiring systems exhibit measurable bias—8.5% disadvantage, amplified at entry level."
2. "Aggregate compliance hides localized harm—intersectional analysis is essential."
3. "Mitigation works—threshold adjustment achieves near-perfect parity without sacrificing performance."
4. "Policy implication: Mandate pre-deployment audits, intersectional reporting, and human oversight for all employment AI."

**Gesture to references:**
> "Our analysis draws on EEOC guidance, EU AI Act provisions, the ACLU complaint against HireVue, and the ongoing Mobley v. Workday litigation."

**Closing:**
> "Thank you. We're happy to take questions."

---

## Q&A Preparation

**Likely questions and suggested responses:**

**Q: "Why did you use FairJob instead of real HireVue data?"**
> "HireVue's data is proprietary and not publicly available. FairJob is a published research dataset designed specifically for fairness analysis in job recommendations—it mirrors the gatekeeping function we're studying."

**Q: "Does the 4/5ths rule actually apply to AI systems?"**
> "Yes. EEOC guidance from 2023 explicitly states that algorithmic decision-making tools are 'selection procedures' under Title VII. The Mobley v. Workday case is testing this in court right now."

**Q: "Isn't threshold adjustment just reverse discrimination?"**
> "No. It's adjusting the decision boundary to ensure equal selection rates—the same outcome a fair process would produce. The underlying model still ranks candidates by predicted fit; we're just correcting for historical bias in where we draw the line."

**Q: "What if the protected attribute isn't available at inference time?"**
> "That's a real implementation challenge. Proxy methods exist, but they raise their own concerns. The more robust solution is reweighing during training, which doesn't require protected attributes at inference."

**Q: "What's the business case for doing this?"**
> "Risk mitigation—litigation is expensive. Talent access—biased systems filter out qualified candidates. And reputation—companies face increasing scrutiny on AI ethics. But honestly, the strongest case is simply: it's the right thing to do, and it's technically feasible."

---

## Timing Summary

| Slide | Topic | Time | Cumulative |
|-------|-------|------|------------|
| 1 | Title | 0:20 | 0:20 |
| 2 | Why It Matters | 0:50 | 1:10 |
| 3 | System Framing | 0:50 | 2:00 |
| 4 | Dataset & Approach | 0:45 | 2:45 |
| 5 | Bias Findings | 0:55 | 3:40 |
| 6 | Aggregate Fairness | 0:50 | 4:30 |
| 7 | Ethics Lens | 0:50 | 5:20 |
| 8 | Sociology Lens | 0:50 | 6:10 |
| 9 | Governance Lens | 0:50 | 7:00 |
| 10 | Mitigation | 0:50 | 7:50 |
| 11 | Accountability | 0:50 | 8:40 |
| 12 | Conclusions | 0:50 | 9:30 |

**Buffer:** 30 seconds for transitions and pacing adjustments.

---

*Notes prepared for MAIB AI 219 presentation — Group 3*
