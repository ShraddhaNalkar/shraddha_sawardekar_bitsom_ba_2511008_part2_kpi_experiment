# shraddha_sawardekar_bitsom_ba_2511008_part2_kpi_experiment

# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

## What This Project Is About

A subscription-based digital product company ran a campaign experiment to see if a new onboarding experience would get more users to convert to paid subscribers. Users were randomly split into two groups, one got the old experience (Control) and one got the new campaign (Treatment). My job was to define the right success metrics, analyse the experiment results, test whether the improvement was statistically real and make a clear recommendation to leadership.

---

## The Dataset

The file `campaign_experiment_data.xlsx` contains one row per user, with 1,408 users total (693 Control, 715 Treatment). Each row tracks what the user did during their first 30 days, whether they visited the landing page, started a trial, completed onboarding, converted to paid, how much revenue they generated, how many support tickets they raised and their engagement score.

**Key columns:**
- `experiment_group` : Control or Treatment
- `converted_to_paid` : 1 if the user became a paying customer, 0 if not
- `revenue_30d` : revenue generated in the first 30 days
- `engagement_score` : a score measuring how active the user was
- `days_to_convert` : only filled in for users who converted
- `support_tickets_30d` : number of support tickets raised
- `refund_requested` : 1 if the user requested a refund

---

## North Star Metric

**Paid Conversion Rate** : the share of users who convert to a paid plan within 30 days.

This is the right metric to focus on because the whole point of the campaign was to convert more users to paid. Every other metric (landing page visits, trial starts, onboarding completion) is just a step on the way to this outcome. If conversion doesn't improve, the campaign didn't do its job.

The risk of focusing only on this: we could improve conversions but end up with lower-quality customers who refund quickly or generate more support costs. That's why we track guardrail metrics alongside.

---

## KPI Tree Summary

The paid conversion rate breaks down into three main driver areas:

**Acquisition Quality** → Are the right users entering the funnel?
- Landing page visit rate, traffic source, device type

**Onboarding Effectiveness** → Do users actually complete the process?
- Trial start rate, onboarding completion rate, engagement score

**Conversion Readiness** → Are users ready to pay?
- Days to convert, plan type, regional and device segment

**Guardrail metrics** (must not get worse):
- Refund rate, support ticket rate, revenue per converted user

See `outputs/kpi_tree.png` for the full diagram.

---

## How I Analysed the Experiment

**Step 1 : Data quality checks**
Checked for duplicates (found 8), missing values (device_type: 18 missing, traffic_source: 24 missing, engagement_score: 14 missing), invalid binary values (none found) and revenue outliers (3 records above ₹5,000 , kept as genuine).

**Step 2 : Added calculated columns**
Added three formula-based columns to `experiment_analysis.xlsx`:
- `conversion_flag` : labels each user as "Converted" or "Not Converted"
- `revenue_flag` : labels revenue as High (>₹500), Low (>₹0), or No Revenue
- `engagement_band` : groups engagement scores into High (≥70), Medium (≥50), Low (<50)

**Step 3 : Computed summary metrics**
Calculated all required metrics for Control vs Treatment, plus breakdowns by region, device type and plan type.

**Step 4 : Ran a hypothesis test**
Used a one-tailed Z-test for proportions to check whether the conversion rate difference was statistically significant. Result: **p = 0.000573** = highly significant.

**Step 5 : Evaluated guardrail metrics**
Looked at refund rate, support tickets and revenue per converted user to check whether the conversion gains came at a hidden cost.

---

## Hypothesis Test Summary

| Item | Detail |
|------|--------|
| Test | One-tailed Z-test for proportions |
| H0 | Treatment conversion rate ≤ Control |
| H1 | Treatment conversion rate > Control |
| Significance level | α = 0.05 |
| Control rate | 3.17% (22 out of 693) |
| Treatment rate | 6.99% (50 out of 715) |
| Z-statistic | 3.2519 |
| P-value | 0.000573 |
| Result | Reject H0 : statistically significant improvement |

The campaign more than doubled the conversion rate and this result is not due to chance.

---

## Guardrail Metrics Considered

| Guardrail | Control | Treatment | Verdict |
|-----------|---------|-----------|---------|
| Refund rate | 0.0% | 0.4% | ⚠ Small but worth watching |
| Support ticket rate | 0.219/user | 0.372/user | ⚠ Significant spike- needs investigation |
| Revenue per converted user | ₹1,630 | ₹770 | ⚠ Drop likely due to plan mix shift |
| Engagement score | 57.0 | 62.9 | ✅ Improved |
| Days to convert | 8.9 days | 6.4 days | ✅ Improved |

The support ticket spike is the main concern. The campaign seems to create some confusion for users that results in more help requests.

---

## Final Recommendation

**Launch the campaign, but investigate and fix the support ticket spike first.**

The conversion improvement is real, large and statistically solid. The campaign works. But the 70% increase in support tickets per user in the Treatment group suggests the new experience is causing friction or confusion somewhere. Launching without addressing this would increase operational costs and risk user satisfaction.

Suggested approach: audit what's driving the support tickets, fix the friction point, then do a phased rollout starting with Free and Mobile users where the lift is strongest.

---

## Assumptions and Limitations

- The 8 duplicate user IDs were flagged but retained — they're less than 1% of the data and unlikely to change the results.
- Missing device_type and traffic_source records were excluded from those specific segment analyses only.
- The revenue per converted user drop may reflect a plan mix difference rather than truly lower-value customers, but this needs confirmation with longer-term data.
- The experiment covers one time period — seasonal or novelty effects can't be fully ruled out.
- No master user list was available to validate user IDs against.

---

## Screenshots Included

| File | What It Shows |
|------|--------------|
| `screenshots/summary_metrics.png` | Control vs Treatment metrics comparison table |
| `screenshots/hypothesis_test_output.png` | Hypothesis test inputs, outputs, and decision |
| `screenshots/kpi_tree_preview.png` | The KPI tree diagram |
