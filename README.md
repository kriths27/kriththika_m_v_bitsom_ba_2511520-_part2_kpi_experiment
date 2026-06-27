# Part 2: KPI Framework, Business Experiment Analysis & Decision

**Student:** Kriththika M V | **ID:** `bitsom_ba_2511520`  
**Tool Stack:** Python 3 (pandas, scipy, statsmodels, xlsxwriter, matplotlib)

---

## Problem Statement

A SaaS company ran an A/B experiment with a new marketing campaign treatment to improve user conversion rates. The dataset contains **1,408 users** (693 Control, 715 Treatment) tracked over a 30-day window with 16 attributes covering funnel behavior, revenue, support load, and engagement.

**Objective:** Build a KPI framework, compute all experiment metrics, run statistical hypothesis tests, evaluate guardrail metrics, and make a data-driven **Launch / No Launch recommendation**.

---

## Repository Structure

```
├── data/
│   └── campaign_experiment_data.xlsx
├── analysis/
│   ├── experiment_analysis.xlsx   ← 4-sheet cleaned + metric workbook
│   └── hypothesis_test_notes.md   ← Hypotheses, p-values, interpretation
├── outputs/
│   ├── kpi_tree.png               ← Full KPI hierarchy visual
│   ├── experiment_summary.xlsx    ← Control vs Treatment all-metrics comparison
│   └── recommendation_memo.md     ← Executive launch decision memo
├── screenshots/
│   ├── summary_metrics.png        ← 6-panel metric comparison bars
│   ├── hypothesis_test_output.png ← Test results + segment breakdowns
│   └── kpi_tree_preview.png       ← KPI tree visual copy
└── README.md
```

---

## Dataset Description

| Attribute | Value |
|---|---|
| Source file | `campaign_experiment_data.xlsx` |
| Total users | 1,408 |
| Control group | 693 users |
| Treatment group | 715 users |
| Observation window | 30 days |
| Missing device_type | 18 (filled → 'Unknown') |
| Missing traffic_source | 24 (filled → 'Unknown') |
| Missing engagement_score | 14 (filled → group median) |
| days_to_convert | Only valid for 72 converters; 1,336 null (non-converters) |

---

## KPI Framework

### North Star Metric ⭐
**Paid Conversion Rate** — Proportion of users who converted to a paid plan within 30 days.

> Justified as the single metric that directly reflects product-market fit, pricing effectiveness, and onboarding quality. All funnel metrics are leading indicators; revenue metrics are lagging consequences.

### KPI Tree Structure

```
⭐ Paid Conversion Rate
├── 📈 Funnel Efficiency
│   ├── Landing Page Visit Rate
│   │   └── Traffic Source Mix, Bounce Rate
│   └── Trial Start & Onboarding Rate
│       └── Days to Convert, Engagement Score
├── 💰 Revenue Generation
│   ├── ARPU (Avg Revenue / User)
│   │   └── Revenue 30d / User, Plan Type Mix
│   └── ARPPU (Rev / Paying User)
│       └── Avg Order Value, Upsell Rate
└── 🛡 Retention & Health
    ├── Refund Rate & Churn Risk
    │   └── Refund Requests, Cancelled Orders
    └── Support Ticket Rate
        └── Ticket Volume, Avg Resolution Time

🛡 GUARDRAIL METRICS
    ├── Refund Rate ≤ 10%
    ├── Support Ticket Rate ≤ 30%
    └── Avg Days to Convert ≤ 20 days
```

---

## Statistical Analysis

### Hypothesis Test — Paid Conversion Rate (Primary)

| Component | Value |
|---|---|
| Test Type | One-tailed Two-Proportion Z-test |
| H₀ | Treatment conversion ≤ Control conversion |
| H₁ | Treatment conversion > Control conversion |
| Control Conversion Rate | 5.34% (37/693) |
| Treatment Conversion Rate | 9.79% (70/715) |
| Z-Statistic | **3.2519** |
| P-Value | **0.000573** |
| α (threshold) | 0.05 |
| **Decision** | ✅ **REJECT H₀ — Statistically Significant** |
| 95% Confidence Interval | Positive — Treatment consistently outperforms |

### Secondary Tests

| Test | Metric | P-Value | Significant? |
|---|---|---|---|
| Welch's t-test | Avg Engagement Score | 0.000000 | ✅ Yes |
| Welch's t-test | ARPU | 0.4578 | ❌ No (revenue per user similar) |

---

## Guardrail Evaluation

| Guardrail | Control | Treatment | Threshold | Result |
|---|---|---|---|---|
| Refund Rate | ~0.4% | 0.4% | ≤ 10% | ✅ PASS |
| Support Ticket Rate | ~27% | 24.8% | ≤ 30% | ✅ PASS |
| Avg Days to Convert | ~6.4d | 6.4d | ≤ 20d | ✅ PASS |

**All 3 guardrails PASSED → Safe to Launch.**

---

## Final Recommendation: 🚀 LAUNCH

The Treatment campaign:
- Produced a **+83% relative lift** in Paid Conversion Rate (statistically significant, p < 0.001)
- Showed **significantly higher engagement** scores across treatment users
- Passed **all 3 guardrail metrics** (refund, support, time-to-convert)
- Directionally improved total 30-day revenue

**Recommended Actions:**
1. Roll out Treatment to 100% of new users
2. Monitor refund rate and support tickets weekly for first 4 weeks post-launch
3. Prioritize Premium plan and Desktop users (highest segment conversion lift)
4. Investigate ARPU gap — engagement is up, but ARPU lift is not yet statistically significant
5. Build 90-day follow-up study to measure LTV impact



*Part of BITSOM BA Capstone Project | Generated: June 2026*
