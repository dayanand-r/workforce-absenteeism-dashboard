
# ❓ Frequently Asked Questions (FAQ)

## Overview

This document answers the most common questions about the Workforce Absenteeism Analytics Dashboard — covering the project's purpose, technical decisions, methodology, and portfolio context.

---

## 📌 General Questions

### What is this project?

This is a **Workforce Absenteeism Analytics Dashboard** built in Advanced Excel with Power Query. It automates attendance tracking, calculates Bradford Factor risk scores, identifies absenteeism patterns, and provides a strategic intervention framework — all with zero code.

### Is this a real project or a tutorial/demo?

This is a **real project** born from an actual workplace need. My manager provided raw attendance data and asked for analysis. Instead of a one-time report, I built a fully automated, interactive dashboard. It was later adopted as an official team project for ongoing use.

### Was this built alone or as a team?

I built this **individually**. The initial request came from my manager, and I designed, developed, and iterated the solution independently across three phases.

### Why is this on GitHub if it's an Excel project?

This repository is a **portfolio case study** — it documents the methodology, architecture, analytical approach, and business value of the project. It showcases data engineering, analytics, visualization, and strategic thinking skills — all of which are relevant regardless of whether the tool is Excel, Power BI, Python, or any other platform.

---

## 🏗️ Architecture Questions

### Why Excel instead of Power BI or Python?

**Pragmatic reasons:**
- **Zero cost** — Excel was already available; no license request or IT approval needed
- **Zero adoption barrier** — the team used Excel daily; no training required
- **Speed to value** — I could build and deliver faster in a familiar tool
- **Sufficient power** — Power Query + Pivot Tables provided everything needed for this use case

Excel was the right tool for this context. The skills and methodology demonstrated (ETL pipelines, risk scoring, multi-layer architecture, intervention frameworks) transfer directly to Power BI, Python, or any other analytics platform.

### Why 9 sheets? Isn't that too many?

Each sheet has **exactly one responsibility** — this is the separation of concerns principle. The benefits:
- **Debuggable** — if a chart is wrong, I know to check the Pivot Backend, not the raw data
- **Extensible** — Phases 2 and 3 added 4 new sheets without modifying any Phase 1 sheets
- **Maintainable** — anyone can follow the data flow through the 4 layers
- **Clean presentation** — the Dashboard sheet only displays; it never calculates

### What are the 4 layers?

| Layer | Sheets | Purpose |
|:------|:-------|:--------|
| **Layer 1: Input** | Attendance Files | Raw data entry point (via Power Query) |
| **Layer 2: Master** | Employee Master, DOJ Data | Reference data for context |
| **Layer 3: Analytics** | Pivot Backend, BF Analysis, DOJ Enrichment, Analysis | All calculations and scoring |
| **Layer 4: Presentation** | Dashboard, Action Plan | Visual interface and recommended actions |

---

## 🧮 Bradford Factor Questions

### What is the Bradford Factor?

The Bradford Factor is an **industry-standard formula** used in HR analytics to measure the impact of employee absenteeism. It was developed at the Bradford University School of Management in the UK.

**Formula: BF = S² × D**
- S = Number of separate absence spells (instances)
- D = Total number of absence days

### Why does it square the spells?

Because **frequent short absences are more operationally disruptive** than infrequent long absences. Example:

| Scenario | Spells | Days | BF Score |
|:---------|:-------|:-----|:---------|
| 1 absence of 10 days | 1 | 10 | **10** |
| 10 absences of 1 day each | 10 | 10 | **1,000** |

Same total days, but 100x higher score for the frequent pattern — correctly reflecting its greater operational disruption.

### What do the risk levels mean?

| BF Score | Risk Level | What It Means | What Happens |
|:---------|:-----------|:-------------|:-------------|
| **0–50** | 🟢 Low Risk | Normal attendance variability | Standard monitoring |
| **51–100** | 🟡 Monitor | Pattern may be developing | Watch for 1–2 months |
| **101–200** | 🟠 Potential Trend | Clear frequent absence pattern | Supportive conversation, identify root causes |
| **201+** | 🔴 High Risk | Chronic disruptive absence | Formal review with documented support plan |

### Are these thresholds universal?

These are the **most widely used Bradford Factor thresholds** in HR analytics globally. They can be recalibrated based on organization-specific data after 6–12 months of tracking.

---

## ⚙️ Technical Questions

### What is Power Query?

Power Query is a **data transformation and ingestion tool** built into Microsoft Excel and Power BI. It allows you to:
- Connect to data sources
- Clean and transform data through a visual interface
- Load processed data into Excel — all without writing code
- Refresh everything with one click

### Why Power Query instead of VBA macros?

| Criteria | Power Query | VBA |
|:---------|:-----------|:----|
| **Learning curve** | Visual, step-by-step | Requires programming |
| **Maintenance** | Self-documenting steps | Code must be read and understood |
| **Security** | No macro security concerns | Macro warnings and security settings |
| **Auditability** | Every step visible | Code review required |
| **Accessibility** | Anyone can use | Only developers can modify |

### How does the one-click refresh work?

1. User clicks **"Refresh All"** in Excel
2. Power Query reconnects to the data source
3. Raw data is extracted and transformed
4. Calculated fields (UPA%, BF Score, etc.) are computed
5. Processed data loads into the Attendance Files sheet
6. All pivot tables auto-refresh
7. All charts auto-update
8. All KPI cards auto-recalculate
9. BF Analysis risk scores auto-update
10. DOJ Enrichment auto-updates

**Result:** The entire dashboard — from raw data to final visuals — updates in seconds.

### Can this handle more employees?

Yes. The architecture is **inherently scalable**:
- Power Query handles any data volume
- Pivot tables automatically expand with new rows
- Excel tables auto-extend formulas to new rows
- No structural changes needed for more employees, months, or years

---

## 📅 Evolution Questions

### Why was it built in three phases?

It wasn't planned that way — **it evolved based on real business needs**:

| Phase | What Triggered It |
|:------|:-----------------|
| **Phase 1** | Manager asked for attendance data analysis |
| **Phase 2** | Need for risk scoring beyond simple UPA% tracking |
| **Phase 3** | Need to understand if tenure correlates with absenteeism patterns |

This iterative approach meant each phase was shaped by real feedback, not assumptions.

### Did Phase 2 break Phase 1?

No. **Phase 1 sheets were never modified** when Phase 2 was added. The Bradford Factor engine was added as new sheets (BF Analysis, Employee Master) that read from the existing Attendance Files sheet. This validates the separation of concerns architecture.

### Did Phase 3 break Phase 2?

No. Same principle — Phase 3 added new sheets (DOJ Data, DOJ Enrichment) without modifying any Phase 1 or Phase 2 sheets. The architecture was designed to be **additive, not destructive**.

---

## 📋 Action Plan Questions

### What is the intervention framework?

A **4-phase, data-driven strategy** for managing workforce absenteeism, directly linked to Bradford Factor risk tiers:

| Phase | BF Trigger | Focus |
|:------|:----------|:------|
| **Phase 1: Preventive Culture** | 0–50 | Maintain healthy patterns through recognition and transparency |
| **Phase 2: Early Intervention** | 51–100 | Catch emerging patterns with check-ins and workload assessment |
| **Phase 3: Targeted Support** | 101–200 | Structured improvement plans, wellness referrals, cross-training |
| **Phase 4: Structured Recovery** | 201+ | Formal review, documented agreements, phased re-integration |

### Is the action plan company-specific?

No. The framework is **universally applicable** — designed using general workforce management best practices. It works for any organization managing absenteeism regardless of industry, size, or location.

### Who uses the action plan?

| Stakeholder | How They Use It |
|:------------|:---------------|
| **Team Leaders** | Follow recommended actions for their team members |
| **HR** | Ensure fair, consistent treatment across the organization |
| **Operations Managers** | Plan staffing and coverage proactively |
| **Leadership** | Review organizational health trends |

---

## 🔒 Compliance & Data Questions

### Is any real employee data included?

**No.** All data in this repository is **anonymized sample data**. Employee names are replaced with generic identifiers (Employee 1, Employee 2, etc.). Team Leader names are replaced similarly. No company names, real identities, or confidential information is included.

### Can I use this for my organization?

Yes — this is licensed under the **MIT License**. You can use, adapt, and build upon this methodology and framework for your own workforce analytics needs. The approach, architecture, and intervention framework are designed to be universally applicable.

### Does this project contain any proprietary methodology?

No. The Bradford Factor is a **publicly documented, industry-standard formula**. The Power Query pipeline uses standard Excel features. The intervention framework is based on general workforce management best practices. Nothing proprietary is included.

---

## 🚀 Future Questions

### Will this be migrated to Power BI?

It's a consideration for the future. Power BI would add:
- Web-based access (no file sharing needed)
- Auto-scheduled data refresh
- Mobile dashboard access
- Better collaboration features

The methodology and architecture would transfer directly — only the platform changes.

### Could machine learning be added?

Yes — potential ML enhancements include:
- **Predictive modeling** — forecast which employees are likely to develop absence patterns
- **Seasonal analysis** — identify high-risk periods automatically
- **Anomaly detection** — flag unusual absence patterns that don't fit expected trends

### Can this scale to thousands of employees?

The methodology scales perfectly. For very large datasets (10,000+ employees), Power BI or a database-backed solution would be more appropriate than Excel — but the Bradford Factor scoring, risk categorization, and intervention framework work identically at any scale.

---

## 📚 Related Documents

- [Presentation Summary](presentation-summary.md) — One-page project overview
- [Solution Design](../docs/solution-design.md) — Complete architecture overview
- [Methodology](../docs/methodology.md) — Analytical approach
- [Bradford Factor Explained](../docs/bradford-factor-explained.md) — Deep dive into BF scoring
- [Business Case](../docs/business-case.md) — Business impact and value
- [Lessons Learned](../docs/lessons-learned.md) — Key reflections
