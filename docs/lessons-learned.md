
# 🧠 Lessons Learned

## Overview

This document captures the key lessons, reflections, and insights gained from building the Workforce Absenteeism Analytics Dashboard across its three iterative phases. These learnings are applicable to anyone building analytics solutions — whether in Excel, Power BI, or any other platform.

---

## 🔑 Top 10 Lessons

### 1. Over-Deliver on the Ask

**The Situation:** Manager asked for attendance data analysis — expected a one-time report with findings.

**What I Did:** Built a fully automated, interactive, reusable dashboard instead.

**The Lesson:** When someone asks for analysis, they usually need more than they're asking for. Delivering a reusable tool instead of a one-time report multiplied the value — the dashboard is still in use, while a static report would have been forgotten in a week.

**Takeaway:** Always ask yourself: *"Can I solve this once in a way that keeps solving it forever?"*

---

### 2. Automate Before You Analyze

**The Situation:** I had a choice — start analyzing immediately or spend time building a Power Query pipeline first.

**What I Did:** Built the Power Query pipeline first, even though it delayed the initial delivery slightly.

**The Lesson:** That upfront investment in automation paid for itself within the first monthly refresh. Every subsequent update took seconds instead of hours. If I had started with manual analysis, I would have been re-doing the same manual work every single month.

**Takeaway:** Invest in the pipeline early. The time you spend automating data ingestion will be returned many times over.

---

### 3. Separate Concerns — Every Sheet Should Have One Job

**The Situation:** It was tempting to put everything — data, calculations, charts, and pivot tables — on one sheet.

**What I Did:** Created a 9-sheet architecture where each sheet has a single, clear responsibility.

**The Lesson:** Separation of concerns made the dashboard:
- **Easier to debug** — if a chart is wrong, I know to check the Pivot Backend, not the raw data
- **Easier to extend** — adding Bradford Factor (Phase 2) and DOJ (Phase 3) didn't require restructuring existing sheets
- **Easier to maintain** — anyone can understand the flow by following the layers

**Takeaway:** Resist the urge to put everything in one place. Clean architecture is the foundation of a sustainable solution.

---

### 4. The Bradford Factor Reveals What UPA% Hides

**The Situation:** Phase 1 used UPA% as the sole metric. Some employees had similar UPA% but vastly different absence behaviors.

**What I Discovered:** An employee with 10 single-day absences is far more disruptive than an employee with one 10-day absence — even though their UPA% is identical.

**The Lesson:** Single metrics create blind spots. The Bradford Factor's S² × D formula captured the pattern dimension that UPA% missed entirely. Without it, the dashboard was informative but not truly insightful.

**Takeaway:** Always question whether your primary metric tells the full story. If it doesn't, find a complementary metric that fills the gap.

---

### 5. Context Changes Everything — Tenure Matters

**The Situation:** Phase 2 flagged employees with high Bradford Factor scores, but the recommended actions felt one-size-fits-all.

**What I Discovered:** A new joiner (3 months) with a BF score of 150 likely needs onboarding support, while a 5-year veteran with the same score may need re-engagement. Same number, completely different root causes.

**The Lesson:** Data without context can lead to wrong conclusions. Adding Date of Joining and tenurity bands in Phase 3 transformed the dashboard from "who has a problem" to "what kind of support does this person need."

**Takeaway:** Always look for contextual dimensions that can change the interpretation of your metrics. Age, tenure, team, location — these all add layers of meaning.

---

### 6. Build for the User, Not for Yourself

**The Situation:** I understood the data model and formulas, but the people using the dashboard (Team Leaders, HR, Operations Managers) might not.

**What I Did:** Designed the Dashboard sheet to be purely visual — charts, KPI cards, and slicers. No raw numbers, no formulas visible, no technical complexity exposed.

**The Lesson:** The best dashboard is one where the user doesn't need to understand how it works. They interact with slicers, read charts, and see recommended actions — the complexity is hidden behind the scenes.

**Takeaway:** Your end user should never have to open a backend sheet. If they do, your dashboard design needs work.

---

### 7. Iteration Beats Perfection

**The Situation:** I could have tried to build the perfect dashboard in Phase 1 — anticipating Bradford Factor, DOJ analysis, and everything else upfront.

**What I Did:** Built Phase 1 as a solid foundation, then added layers as requirements emerged naturally.

**The Lesson:** Iterative delivery had three major benefits:
- **Faster initial value** — Phase 1 was useful immediately
- **User-driven evolution** — Phases 2 and 3 were shaped by real feedback, not assumptions
- **Lower risk** — Each phase was manageable in scope

**Takeaway:** Don't try to build everything at once. Ship a solid V1, learn from real usage, and iterate. Each phase should add value without breaking what came before.

---

### 8. Action Plans Are More Valuable Than Dashboards

**The Situation:** The dashboard was visually impressive and analytically sound, but the natural question from stakeholders was: *"OK, so what do we DO about this?"*

**What I Did:** Added a data-driven intervention framework directly linked to Bradford Factor risk tiers — so every score comes with a clear recommended action.

**The Lesson:** A dashboard that shows you the problem is useful. A dashboard that shows you the problem AND tells you what to do about it is invaluable. The intervention framework turned the dashboard from a monitoring tool into a decision-making tool.

**Takeaway:** Always ask: *"What action will someone take after seeing this data?"* If the answer is unclear, your dashboard is incomplete.

---

### 9. Power Query Is Underrated

**The Situation:** Most people in the team used Excel for manual data entry and formula-based calculations. Power Query was not widely used.

**What I Discovered:** Power Query fundamentally changed the architecture — it meant:
- Data ingestion was automated and error-free
- The same pipeline worked regardless of data volume
- Transformations were documented and auditable
- Monthly updates became a non-event

**The Lesson:** Power Query is perhaps the most underrated tool in Excel. It bridges the gap between Excel and enterprise-grade ETL tools — providing automation, consistency, and scalability without requiring a single line of code.

**Takeaway:** If you're doing any repetitive data processing in Excel, learn Power Query. It will transform your workflow.

---

### 10. Self-Initiated Projects Have Outsized Impact

**The Situation:** Nobody asked me to build a dashboard. The request was for a simple analysis.

**What Happened:** By exceeding the ask, the project was adopted as an official team initiative. It became a recurring tool rather than a forgotten report.

**The Lesson:** Self-initiated improvements demonstrate more than technical skill. They show:
- **Initiative** — you see opportunities others don't
- **Ownership** — you care about outcomes, not just tasks
- **Business thinking** — you understand what creates lasting value
- **Leadership** — you don't wait to be told what to do

**Takeaway:** The most impactful projects are often the ones nobody asked for. If you see a better way, build it.

---

## 📊 Technical Lessons Summary

| Area | Lesson | Impact |
|:-----|:-------|:-------|
| **Power Query** | Automate data ingestion before doing any analysis | Saved hours every month |
| **Architecture** | Separate concerns — one sheet, one responsibility | Made the dashboard extensible and maintainable |
| **Metrics** | One metric is never enough — complement UPA% with Bradford Factor | Revealed hidden patterns |
| **Context** | Add contextual dimensions (tenure, team) to enrich interpretation | Enabled targeted interventions |
| **Formulas** | Use IF-based automation for risk categorization | Eliminated manual judgment |
| **Visualization** | Keep the dashboard visual-only — hide complexity in backend sheets | Made it accessible to non-technical users |
| **Design** | Build for iteration, not perfection | Faster delivery, better fit, lower risk |

---

## 🔄 What I Would Do Differently

| Aspect | What I Did | What I'd Do Differently |
|:-------|:-----------|:-----------------------|
| **Documentation** | Documented after building | Document design decisions during the build process |
| **User testing** | Delivered and iterated based on feedback | Would involve end users earlier in the design phase |
| **Threshold calibration** | Used industry-standard BF thresholds | Would calibrate thresholds based on organization-specific data after 6 months |
| **Predictive element** | Dashboard is descriptive (shows what happened) | Would add predictive component (forecast future risk periods) |
| **Platform choice** | Built in Excel | Would evaluate Power BI earlier for web-based access and collaboration |

---

## 💡 Advice for Others Building Similar Solutions

1. **Start with the question, not the tool** — Understand what stakeholders need to know before deciding how to show it
2. **Automate first** — The pipeline is more important than the dashboard
3. **Design for non-technical users** — If your stakeholder needs training to use your dashboard, simplify it
4. **Include "so what"** — Every insight should come with a recommended action
5. **Iterate based on real feedback** — Don't guess what people need; build, ship, learn, improve
6. **Separate data from presentation** — Backend and frontend should be independent layers
7. **Think about sustainability** — Who maintains this after you? Make it easy for them
8. **Document your decisions** — Future-you (and your replacement) will thank you

---

## 📚 Related Documents

- [Solution Design](solution-design.md) — The architecture these lessons shaped
- [Methodology](methodology.md) — The analytical approach that evolved through these learnings
- [Business Case](business-case.md) — The business value these lessons helped maximize
- [Design Decisions](../architecture/design-decisions.md) — Specific choices influenced by these lessons
- [FAQ](../resources/faq.md) — Questions that often arise from these learnings
