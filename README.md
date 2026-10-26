# Global Project Portfolio Monitoring & Variance Analytics (Power BI)

## 📌 Business Overview
This project delivers an interactive executive BI dashboard for **Sanitoral**, an international organization managing concurrent IT and Marketing project portfolios across multiple countries. The objective is to centralize strategic performance tracking, automate data refresh workflows, and provide actionable drill-down capabilities across three leadership tiers (Executive, Regional, Country).

---

## 🎯 Framing & User Stories (Product Strategy Canvas)
Developed using a structured framework tailored to three distinct management personas:
- **CEO / General Management:** High-level portfolio health, total active vs. delayed projects, overall budget drift, and domain filtering (IT vs. Marketing).
- **Regional Directors:** Geographic map distribution, regional delay bottlenecks, and localized project intervention triggers.
- **Country Managers:** Granular phase-level tracking (Phases 1–4 for Marketing, Phases A–F for IT), core KPI variances, and interactive tooltips for project details.

![Product Strategy Canvas](./project_strategy_canvas.png)

---

## ⚙️ Automated ETL Architecture (Power Query)
- **Zero-Manual Preprocessing:** Automated data cleansing and shaping pipeline executed entirely in Power Query M-code.
- **Relational Composite Keys:** Built surrogate unique keys `[Phase - Project ID]` via column mergers to bridge project baseline plans and actual execution records without altering raw files.
- **Scalable Refresh:** Automated transformation steps designed to handle recurring updates with zero loss of data integrity.

![Power Query Steps](./etl_steps.png)

---

## 🗄️ Data Model & Architecture
Implemented a normalized Star Schema designed for optimal analytical performance and clear filter propagation:
- **Central Fact Table (Plan):** `Projects_plans`
- **Fact Tables (Actuals):** `Actual_Costs`, `Actual_Duration`, `Actual_Deliverable`
- **Dimension Tables:** `Country_Profiles`, `Projects_Locations`, `Project type`
- **Dedicated Measure Table:** ` Mesures` (isolating all DAX business calculations)

![Data Model](./data_model.png)

---

## 📈 DAX Analytics & Governance
All analytical formulas and variance metrics are isolated and fully documented in [`dax_measures.md`](./dax_measures.md).

Key analytical logic implemented:
- **Variance Tracking:** Planned vs. actual calculations across Cost, Duration, and Deliverables (in absolute values and percentages).
- **Automated Risk Flags:** Dynamic conditional alerts flagging any project with $\ge 15\%$ drift on deadlines, budgets, or milestone deliveries.
- **Custom Visuals & UX:** Custom **Gantt Chart** timeline visualization, natural language Q&A querying, and contextual hover tooltips.

---

## 📁 Repository Structure

- `Sanitoral-Project_Monitoring.pbix` : Full interactive Power BI report (embedded VertiPaq model and visuals)
- `dax_measures.md` : Documented DAX analytics script and formulas
- `project_strategy_canvas.png` : Business requirements and user stories matrix
- `data_model.png` : Star schema relational data model
- `etl_steps.png` : Automated Power Query ETL pipeline
- `README.md` : Project documentation
