# SearchXP — A/B Testing Analysis Framework

> Modeled on how Google validates search ranking algorithm changes before shipping to billions of users.

## Project Overview

SearchXP is an end-to-end A/B testing analysis framework that simulates and analyzes a search ranking experiment. The core question it answers:

**Did a new search ranking algorithm genuinely help users find what they were looking for — or did we just think it did?**

## Results Summary

| Metric | Control | Treatment | Lift | Significant? |
|--------|---------|-----------|------|-------------|
| CTR | 48.48% | 54.89% | +6.41% | Yes (p < 0.001) |
| Avg Dwell Time | 151.29s | 180.71s | +29.42s | Yes (p < 0.001) |
| Bounce Rate | 34.88% | 25.17% | -9.71% | Yes (p < 0.001) |

**Verdict: Ship the new algorithm.** 95% CI for CTR lift: [5.02%, 7.79%]

## Tech Stack
Python, NumPy, Pandas, SciPy, SQLite, SQL, Matplotlib, Tableau

## Phases
- Phase 1: Data Simulation — 10,000 users, 21 days
- Phase 2: SQL Analysis — 5 business queries
- Phase 3: Hypothesis Testing — Chi-square, T-test, Cohen's d
- Phase 4: Advanced Checks — Novelty effect, SRM, Confidence intervals
- Phase 5: Tableau Dashboard

## About
Built by Pooja Chavanpatil — MS Statistical Data Science, SFSU
