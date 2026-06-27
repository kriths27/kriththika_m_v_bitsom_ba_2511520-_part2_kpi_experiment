# Hypothesis Test Notes — A/B Experiment Analysis
**Student:** Kriththika M V | **ID:** bitsom_ba_2511520  
**Dataset:** `campaign_experiment_data.xlsx`  
**Date:** 27 June 2026

---

## 1. North Star Metric

**Paid Conversion Rate** — the proportion of users who converted to a paid plan within 30 days.

**Justification:**  
This is the single most direct measure of business value for a SaaS product. It sits at the intersection of product quality, onboarding effectiveness, and pricing power. All other funnel metrics (landing page visits, trial starts, onboarding completions) are *leading indicators* that feed into this metric. Revenue (ARPU/ARPPU) is a *consequence* of conversion. Paid Conversion Rate is the most controllable, most actionable, and most directly linked to unit economics.

---

## 2. Hypotheses

### Primary Test — Paid Conversion Rate

| | Statement |
|---|---|
| **H₀ (Null)** | The Treatment campaign does NOT improve paid conversion rate. `P(convert | Treatment) ≤ P(convert | Control)` |
| **H₁ (Alternative)** | The Treatment campaign DOES improve paid conversion rate. `P(convert | Treatment) > P(convert | Control)` |

**Test Type:** One-tailed two-proportion Z-test  
**Significance Level (α):** 0.05  
**Test Direction:** One-sided (right tail — we test if Treatment > Control)

### Secondary Test 1 — Avg Engagement Score

| | Statement |
|---|---|
| **H₀** | Treatment does NOT produce higher engagement scores. |
| **H₁** | Treatment produces statistically higher engagement scores. |

**Test Type:** One-tailed Welch's t-test (unequal variance)

### Secondary Test 2 — ARPU

| | Statement |
|---|---|
| **H₀** | Treatment does NOT produce higher average revenue per user. |
| **H₁** | Treatment produces statistically higher ARPU. |

**Test Type:** One-tailed Welch's t-test

---

## 3. Results

### Primary: Paid Conversion Rate (Z-Test)

| Metric | Control | Treatment |
|---|---|---|
| User Count | 693 | 715 |
| Converters | 22 | 50 |
| Conversion Rate | 0.0317 (3.17%) | 0.0699 (6.99%) |
| Absolute Lift | — | **+0.0382** |
| Relative Lift | — | **+120.28%** |
| Z-Statistic | — | **3.2519** |
| P-Value | — | **0.000573** |
| 95% CI (difference) | — | [0.0154, 0.0610] |
| **Decision** | — | **✅ REJECT H₀ — Statistically Significant** |

### Secondary: Avg Engagement Score (t-Test)

| | Value |
|---|---|
| Control Mean | 57.021 |
| Treatment Mean | 62.928 |
| t-Statistic | 8.0264 |
| P-Value | 0.000000 |
| Decision | ✅ Significant improvement in engagement |

### Secondary: ARPU (t-Test)

| | Value |
|---|---|
| Control ARPU | ₹51.7493 |
| Treatment ARPU | ₹53.8751 |
| t-Statistic | 0.1060 |
| P-Value | 0.457783 |
| Decision | ❌ No significant ARPU difference |

---

## 4. Interpretation

The p-value of **0.000573** is LESS THAN the significance threshold of 0.05. We **REJECT the null hypothesis**. This means the Treatment campaign produced a statistically significant improvement in Paid Conversion Rate. The probability of observing this result by chance alone is less than 5%."

The 95% confidence interval for the difference in conversion rates is **[0.0154, 0.0610]**, meaning the true uplift from the Treatment campaign lies within this range with 95% confidence.

---

## 5. Assumptions & Limitations

1. **Independence:** Users in Control and Treatment groups are assumed to be independent (no cross-contamination).
2. **Random Assignment:** Experiment groups are assumed to be randomly assigned (not self-selected).
3. **Sample Size Adequacy:** With n=693 (Control) and n=715 (Treatment), the test has adequate power for detecting moderate effect sizes.
4. **30-Day Window:** All revenue and conversion metrics are measured within a 30-day window — this may not capture long-tail conversions.
5. **Missing `days_to_convert`:** 1336 records have null days_to_convert — these are non-converters and are correctly excluded from the average.

---
*Part 2 Analysis | BITSOM BA Capstone | bitsom_ba_2511044*
