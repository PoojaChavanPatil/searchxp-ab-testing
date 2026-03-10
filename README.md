# SearchXP — A/B Testing Analysis Framework

> Modeled on how Google validates search ranking algorithm changes before shipping to billions of users.

---

## Project Overview

SearchXP is an end-to-end A/B testing analysis framework that simulates and analyzes a search ranking experiment. The core question it answers:

> **Did a new search ranking algorithm genuinely help users find what they were looking for — or did we just think it did?**

This project covers the full experimentation lifecycle: data simulation, SQL analysis, statistical hypothesis testing, advanced experiment validation, and stakeholder dashboard.

---

## Results Summary

| Metric | Control | Treatment | Lift | Significant? |
|--------|---------|-----------|------|-------------|
| CTR | 48.48% | 54.89% | +6.41% | Yes (p < 0.001) |
| Avg Dwell Time | 151.29s | 180.71s | +29.42s | Yes (p < 0.001) |
| Bounce Rate | 34.88% | 25.17% | -9.71% | Yes (p < 0.001) |
| Position 1 Clicks | 40.51% | 55.07% | +14.56% | — |

**Verdict: Ship the new algorithm.** All metrics improved significantly. No novelty effect detected. 95% CI for CTR lift: [5.02%, 7.79%].

---

## Project Structure

```
SearchXP/
│
├── phase1_simulate_data.ipynb    # Data simulation — 10,000 users, 21 days
├── phase2_sql.ipynb              # SQL queries — 5 business questions
├── phase3_statistics.ipynb       # Hypothesis testing — chi-square, t-test, Cohen's d
├── phase_04.ipynb                # Advanced checks — novelty effect, SRM, CI
├── phase5_export.ipynb           # Dashboard data export
│
├── search_experiment.csv         # Simulated experiment dataset (20,013 rows)
├── result_ctr.csv                # CTR by group
├── result_dwell.csv              # Dwell time by group
├── result_bounce.csv             # Bounce rate by group
├── result_daily_trend.csv        # Daily CTR over 21 days
├── result_positions.csv          # Click position distribution
├── result_weekly_ctr.csv         # Weekly CTR summary
│
├── pbi_kpi_summary.csv           # Dashboard: KPI summary
├── pbi_daily_trend.csv           # Dashboard: Daily trend
├── pbi_click_position.csv        # Dashboard: Click positions
├── pbi_confidence_interval.csv   # Dashboard: Confidence interval
└── pbi_weekly_trend.csv          # Dashboard: Weekly trend
```

---

## Methodology

### Phase 1 — Data Simulation
Simulated a realistic 10,000-user search experiment across 21 days. Each user was randomly assigned to control (old algorithm) or treatment (new algorithm). Behavioral signals simulated: click-through rate, dwell time, bounce rate, and click position. Noise was added intentionally to reflect real-world variance.

### Phase 2 — SQL Analysis
Loaded data into SQLite and wrote 5 business queries answering:
- Overall CTR per group
- Average dwell time (clicked sessions only)
- Bounce rate per group
- Daily CTR trend over 21 days
- Click position distribution

### Phase 3 — Statistical Hypothesis Testing
| Metric | Test | Statistic | P-Value | Result |
|--------|------|-----------|---------|--------|
| CTR | Chi-Square | 81.96 | < 0.000001 | Significant |
| Dwell Time | T-Test | -24.87 | < 0.000001 | Significant |
| Bounce Rate | Chi-Square | 223.89 | < 0.000001 | Significant |
| Effect Size | Cohen's d | 0.49 | — | Medium |

### Phase 4 — Advanced Experiment Validation
Three checks that real experimentation teams run before shipping:

**1. Novelty Effect Detection**
Tracked weekly CTR gap across 3 weeks. Gap grew from 3.90% (Week 1) to 7.66% (Week 3) — no novelty effect detected. Treatment advantage is durable.

**2. Sample Ratio Mismatch (SRM)**
Chi-square goodness-of-fit test on group sizes. Chi2 = 0.07, p = 0.79. No SRM detected — randomization is valid.

**3. Practical Significance**
95% Confidence Interval on CTR lift: [5.02%, 7.79%]. Even the conservative lower bound represents a meaningful business improvement.

### Phase 5 — Tableau Dashboard
Built an interactive dashboard in Tableau Public with:
- Control vs Treatment grouped bar chart (all 3 metrics)
- 21-day CTR trend line chart

---

## Tech Stack

| Tool | Usage |
|------|-------|
| Python | Data simulation, statistical analysis |
| NumPy / Pandas | Data manipulation |
| SciPy | Chi-square test, T-test |
| SQLite / SQL | Data querying |
| Matplotlib | Exploratory plots |
| Tableau Public | Interactive dashboard |

---

## Key Concepts Demonstrated

- A/B experiment design and user randomization
- Behavioral metric selection (CTR, dwell time, bounce rate)
- Chi-square test for proportions
- Independent samples T-test for means
- Cohen's d effect size interpretation
- Novelty effect detection via time series analysis
- Sample Ratio Mismatch (SRM) validation
- Confidence interval construction for practical significance
- Stakeholder-facing dashboard design

---

## Business Context

This project mirrors the experimentation workflow used by Google's Search Quality team, Microsoft's Bing team, and Amazon's A9 search team. Before any ranking change ships to production, teams run exactly these checks — statistical significance, novelty effect analysis, SRM validation, and practical significance assessment.

---

## About

Built by **Pooja Chavanpatil**
MS in Statistical Data Science — San Francisco State University

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Pooja%20Chavanpatil-blue?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/poojachavanpatil/)
[![Portfolio](https://img.shields.io/badge/Portfolio-pooja--portfolio2026.vercel.app-blue?style=flat-square)](https://pooja-portfolio2026.vercel.app)
