# Hypothesis Test Notes

## What We're Testing

The company ran an experiment where some users got the old onboarding experience (Control) and others got the new campaign experience (Treatment). We want to know: did the new campaign actually help more users convert to paid subscribers or did it just look better by chance?

To answer that properly, we need a formal statistical test, not just eyeballing the numbers.

---

## The Hypotheses

**Null Hypothesis (H0):**
The new campaign does not improve the paid conversion rate. Any difference we see between the two groups is just random variation.

> In plain terms: the campaign made no real difference.

**Alternate Hypothesis (H1):**
The new campaign genuinely improves the paid conversion rate. The Treatment group converts at a higher rate than the Control group.

> In plain terms: the campaign actually works.

---

## Test Setup

| Setting | Choice | Reason |
|---------|--------|--------|
| Test type | One-tailed Z-test for proportions | We're only checking if Treatment is *better*, not just different |
| Direction | One-tailed (right tail) | H1 is specifically that Treatment > Control |
| Significance level | α = 0.05 | Standard business threshold — we accept a 5% chance of a false positive |
| Metric tested | Paid conversion rate | This is the primary success metric (North Star) |

**Why paid conversion rate?**
It's the most direct measure of whether the campaign achieved its goal. Everything else, landing page visits, trial starts, onboarding completions, is a stepping stone. Conversion is what actually generates revenue.

---

## Test Inputs

| Input | Control | Treatment |
|-------|---------|-----------|
| Users in group | 693 | 715 |
| Users who converted to paid | 22 | 50 |
| Conversion rate | 3.17% | 6.99% |

---

## Test Output

| Result | Value |
|--------|-------|
| Z-Statistic | 3.2519 |
| P-Value | 0.000573 |
| Significant at α = 0.05? | **YES** |
| Decision | **Reject the null hypothesis** |

---

## What the Numbers Mean

The p-value of **0.000573** means there is less than a 0.06% chance that this difference happened by random luck. In other words, we are over 99.9% confident that the new campaign genuinely drove more conversions.

The Z-statistic of **3.25** is well above the critical value of 1.645 for a one-tailed test at α = 0.05. This confirms the result is statistically significant.

The relative lift is **+121%** = Treatment converted at more than double the rate of Control (6.99% vs 3.17%).

---

## Business Interpretation

The test result is clear: the new onboarding campaign works. It significantly improved the proportion of users who converted to paid, and the result is not due to chance.

However, statistical significance alone is not enough to make a launch decision. The test only tells us the conversion rate improved. We also need to check whether the quality of those conversions held up specifically, whether revenue per converted user, refund rates and support burden changed in ways that offset the conversion gains.

See the Guardrail Metrics section of the recommendation memo for that analysis.

---

## Interpretation Logic Summary

- If p < 0.05 → Reject H0 → Treatment is significantly better → Evidence supports launch
- If p ≥ 0.05 → Fail to reject H0 → No significant improvement → Do not launch based on this data

In our case: **p = 0.000573 < 0.05 → Reject H0 → Campaign shows significant improvement in conversion rate**
