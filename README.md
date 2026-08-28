
<div align="center">

# 📊 Workforce Absenteeism Analytics Dashboard

### Turning Raw Attendance Data into Actionable Workforce Intelligence

[![Excel](https://img.shields.io/badge/Built%20With-Advanced%20Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/excel)
[![Power Query](https://img.shields.io/badge/Data%20Pipeline-Power%20Query-F2C811?style=for-the-badge&logo=microsoft&logoColor=black)](https://learn.microsoft.com/en-us/power-query/)
[![Bradford Factor](https://img.shields.io/badge/Analytics-Bradford%20Factor-DC3545?style=for-the-badge)](https://en.wikipedia.org/wiki/Bradford_Factor)
[![Pivot Tables](https://img.shields.io/badge/Engine-Pivot%20Tables-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)](https://support.microsoft.com/en-us/office/create-a-pivottable)
[![No Code](https://img.shields.io/badge/Approach-No%20Code-8B5CF6?style=for-the-badge)](https://en.wikipedia.org/wiki/No-code_development_platform)

---

*A comprehensive, interactive Excel dashboard that automates attendance tracking, calculates Bradford Factor risk scores, identifies absenteeism trends, and provides actionable intervention strategies — built entirely with Advanced Excel, Power Query, and no code.*

</div>

---

## 📌 The Story

My manager handed me raw attendance data and asked for analysis — just findings and insights.

Instead of a one-time report, I built **a fully automated, interactive dashboard** that:
- Ingests raw attendance data automatically via Power Query
- Calculates UPA (Unplanned Absence) percentages per employee per month
- Computes Bradford Factor scores to identify absenteeism risk patterns
- Visualizes trends across time, teams, and individuals
- Generates automated risk categorization and recommended actions
- Includes a 3-phase strategic action plan to reduce absenteeism

**What started as a simple data request became an official project** — adopted by the team for ongoing workforce analytics and absenteeism reduction.

---

## 🧠 The Problem

Workforce absenteeism was being tracked manually with no systematic analysis:

| Challenge | Impact |
|:----------|:-------|
| No visibility into absenteeism patterns | Trends went undetected until they became critical |
| No risk scoring mechanism | Couldn't distinguish between occasional and chronic absenteeism |
| Manual data compilation | Time-consuming and error-prone monthly reporting |
| No team-level comparison | Couldn't identify which teams needed intervention |
| Reactive approach | Issues addressed only after significant impact on operations |
| No actionable framework | Data existed but didn't translate into decisions |

---

## ✅ The Solution

A **9-sheet, multi-layer Excel dashboard** with automated data pipeline, analytics engine, and interactive visualization:

```mermaid
graph LR
    A[📁 Raw Attendance Data] -->|Power Query| B[⚙️ Attendance Files]
    B --> C[🔄 Pivot Backend]
    C --> D[📊 Dashboard]
    B --> E[🧮 BF Analysis]
    E --> F[📋 DOJ Enrichment]
    G[👥 Employee Master] --> E
    H[📅 DOJ Data] --> F
    C --> I[📈 Analysis Sheet]
    D --> J[📌 Action Plan]
