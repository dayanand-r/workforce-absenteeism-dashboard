
# 🧮 Bradford Factor — Explained

## Overview

The Bradford Factor is a widely used formula in Human Resource management and workforce analytics that helps organizations measure and assess the impact of employee absenteeism. It was developed at the Bradford University School of Management in the UK and has since become a global standard for absence management.

This document explains the formula, the theory behind it, how it was implemented in this dashboard, and why it was chosen over alternative approaches.

---

## 📐 The Formula

```
BF = S² × D
```

| Component | Meaning | Example |
|:----------|:--------|:--------|
| **S** | Number of **separate absence spells** (instances) within a defined period | An employee who was absent on 3 different occasions has S = 3 |
| **D** | Total number of **absence days** across all spells within the same period | If those 3 occasions totaled 7 days, D = 7 |
| **BF** | The resulting **Bradford Factor score** | BF = 3² × 7 = 9 × 7 = **63** |

---

## 🧠 The Theory: Why S Is Squared

The Bradford Factor's core insight is that **frequent, short, unplanned absences cause more operational disruption than infrequent, longer absences** — even when the total days absent are identical.

### The Logic

| Impact Area | One Long Absence | Many Short Absences |
|:------------|:----------------|:-------------------|
| **Planning** | Team adjusts once, redistributes work | Team must scramble repeatedly, often with no notice |
| **Coverage** | Backup arranged once | Backup needed multiple times, often last-minute |
| **Workflow** | One handover, one catch-up | Multiple handovers, constant context-switching |
| **Morale** | Colleagues understand (medical, etc.) | Repeated pattern may cause resentment or suspicion |
| **Predictability** | Absence timeline often known | Next absence is unpredictable |
| **Cost** | One set of overtime/coverage costs | Repeated overtime/coverage costs compound |

By **squaring S** (the number of spells), the formula mathematically weights frequent absences more heavily than total days alone.

---

## 📊 Real-World Comparison

Here are 5 scenarios with the **same total absence days (10 days)** but vastly different Bradford Factor scores:

| Scenario | Description | Spells (S) | Days (D) | BF Score | Risk Level |
|:---------|:-----------|:-----------|:---------|:---------|:-----------|
| **A** | One absence of 10 consecutive days | 1 | 10 | 1² × 10 = **10** | 🟢 Low Risk |
| **B** | Two absences (5 days each) | 2 | 10 | 2² × 10 = **40** | 🟢 Low Risk |
| **C** | Five absences (2 days each) | 5 | 10 | 5² × 10 = **250** | 🔴 High Risk |
| **D** | Ten absences (1 day each) | 10 | 10 | 10² × 10 = **1,000** | 🔴 High Risk |
| **E** | Twenty half-day absences | 20 | 10 | 20² × 10 = **4,000** | 🔴 High Risk |

**Key Takeaway:** Scenario A and Scenario D have the exact same total absence days, but Scenario D's BF score is **100x higher** — correctly reflecting its significantly greater operational impact.

---

## 📏 Risk Thresholds

The dashboard implements the following industry-standard thresholds:

### Threshold Table

| BF Score Range | Risk Level | Color Code | Interpretation | Recommended Action |
|:---------------|:-----------|:-----------|:---------------|:-------------------|
| **0–50** | Low Risk | 🟢 Green | Normal attendance variability — no pattern of concern | No action needed. Continue standard monitoring |
| **51–100** | Monitor Closely | 🟡 Yellow | Early signs of a pattern — may be developing | Watch over next 1–2 months. Note if frequency is increasing |
| **101–200** | Potential Trend | 🟠 Orange | Clear pattern of frequent absence — not yet critical but concerning | Supportive 1:1 conversation. Identify root causes. Connect with wellness resources if needed |
| **201+** | High Risk | 🔴 Red | Chronic, disruptive absence pattern — significant operational impact | Formal documented review. Create structured improvement plan with milestones |

### Why These Specific Thresholds?

| Reason | Explanation |
|:-------|:-----------|
| **Industry standard** | These bands are the most widely used Bradford Factor thresholds in HR analytics globally |
| **Progressive response** | Each tier escalates the response — from monitoring to support to formal action |
| **Support-first approach** | The framework emphasizes understanding root causes and providing support before any disciplinary action |
| **Operational alignment** | Thresholds correspond to measurable levels of operational disruption |

---

## ⚙️ Implementation in This Dashboard

### How BF Is Calculated

1. **Raw Data Input:** Power Query loads attendance records with Absence Days (D) and Absence Spells (S) pre-calculated per employee per month
2. **BF Calculation:** The `BF Analysis` sheet computes `S² × D` for each employee
3. **Aggregation:** Average BF score is calculated per employee across all available months
4. **Categorization:** IF-based formulas automatically assign risk level and recommended action
5. **Visualization:** Scores feed into the dashboard for visual representation

### Formula Logic Used

```
Risk Category:
  IF Average BF > 200  → "High Risk — Formal Review"
  IF Average BF > 100  → "Potential Trend — Informal Chat / Wellness Check"
  IF Average BF > 50   → "Monitor Closely — Watch for Patterns"
  ELSE                  → "Low Risk — Standard Employee Attendance"
```

### What Makes This Implementation Effective

| Feature | Benefit |
|:--------|:-------|
| **Fully automated** | BF scores calculate automatically — no manual judgment needed |
| **Always current** | Refreshing data via Power Query updates all BF scores instantly |
| **Action-oriented** | Every score comes with a specific recommended response |
| **Contextual** | BF scores are shown alongside UPA%, Team Leader, and Tenure data |
| **Transparent** | Stakeholders can see the raw numbers (S and D) alongside the BF score |

---

## 🔄 Bradford Factor vs. Alternative Approaches

### Why Bradford Factor Was Chosen Over Alternatives

| Approach | How It Works | Limitation | Bradford Factor Advantage |
|:---------|:------------|:-----------|:-------------------------|
| **Simple Absence Count** | Count total days absent | Treats 1 absence of 10 days the same as 10 absences of 1 day | BF distinguishes frequency from duration |
| **Absence Rate (UPA%)** | Absent days ÷ Working days | Same blind spot — doesn't capture pattern | BF captures the pattern, not just the volume |
| **Lost Time Rate** | Total hours lost ÷ Total scheduled hours | Focuses on time lost, not disruption caused | BF focuses on operational disruption |
| **Frequency Rate** | Number of absence episodes ÷ Headcount | Ignores duration entirely | BF balances both frequency AND duration |
| **Custom Scoring** | Organization-defined scoring | Subjective, varies between companies | BF is standardized and globally recognized |

### Bradford Factor Limitations (Acknowledged)

| Limitation | How This Dashboard Addresses It |
|:-----------|:-------------------------------|
| **Doesn't capture reason for absence** | Dashboard is paired with supportive intervention framework — conversations uncover reasons |
| **Can penalize genuine illness** | Support-first approach: wellness check before any formal action |
| **Doesn't account for tenure** | Phase 3 added DOJ analysis — tenure context is now included alongside BF scores |
| **Monthly calculation may miss long-term patterns** | Average BF across months provides a rolling view |
| **One-size-fits-all thresholds** | Thresholds can be recalibrated annually based on organizational norms |

---

## 🌍 Bradford Factor in Practice

The Bradford Factor is used by organizations worldwide across multiple industries:

| Industry | How It's Used |
|:---------|:-------------|
| **Healthcare** | Monitoring staff absence in hospitals where coverage is critical |
| **Contact Centers / BPO** | Tracking agent attendance to maintain SLA commitments |
| **Manufacturing** | Ensuring production line staffing meets operational requirements |
| **Retail** | Managing shift-based workforce attendance |
| **Financial Services** | Maintaining compliance and service levels |
| **Public Sector** | Government agencies use BF as part of attendance management policies |

---

## 📈 How to Read BF Scores in the Dashboard

When reviewing the BF Analysis in the dashboard:

1. **Sort by BF Score (highest first)** — focus attention on the top of the list
2. **Check the Risk Level** — color-coded for instant recognition
3. **Cross-reference with UPA%** — high BF + high UPA% = urgent attention needed
4. **Check Tenure (DOJ tab)** — is this a new joiner struggling or a tenured employee disengaging?
5. **Review the Team Leader** — are multiple high-BF employees under the same TL?
6. **Follow the Recommended Action** — the dashboard tells you exactly what to do next

---

## 📚 Related Documents

- [Methodology](methodology.md) — Overall analytical approach
- [Solution Design](solution-design.md) — Complete architecture overview
- [Power Query Pipeline](power-query-pipeline.md) — How data flows into BF calculations
- [Dashboard Architecture](../architecture/dashboard-architecture.md) — Where BF Analysis fits in the 9-sheet structure
- [Design Decisions](../architecture/design-decisions.md) — Why Bradford Factor was chosen
