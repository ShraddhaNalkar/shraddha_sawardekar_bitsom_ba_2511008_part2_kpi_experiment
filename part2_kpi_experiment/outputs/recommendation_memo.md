# Recommendation Memo

**To:** Leadership / Product Decision Team
**From:** Business Analyst
**Subject:** Should we launch the new onboarding campaign to all users?
**Date:** June 2026

---

## Executive Summary

We ran an A/B test of the new onboarding and activation campaign. The results show a clear and statistically significant improvement in paid conversions,  the Treatment group converted at 7.0% compared to 3.2% in the Control group, which is more than double the rate.

**My recommendation: Launch the campaign, but address the support ticket issue first.**

The conversion improvement is real and the data is solid. But one guardrail metric, support ticket, showed a concerning spike in the Treatment group that needs to be understood before a full rollout. The campaign may be creating confusion or unmet expectations for some users.

---

## The Business Problem

The company wants to improve how many users convert from free/trial to paid subscriptions during the first 30 days after signup. The current onboarding experience leaves too many users dropping off before they reach the paid step.

**Decision to make:** Should we replace the old onboarding experience with the new campaign experience for all users?

**Who it affects:** Every new user who signs up going forward.

**What we need to see to say yes:**
- Conversion rate meaningfully higher in Treatment
- No serious damage to revenue quality or user satisfaction
- Consistent improvement across key user segments

---

## North Star Metric

**Paid Conversion Rate** : the percentage of users who convert to a paid plan within 30 days.

This is the right North Star because it directly measures whether the campaign achieved its purpose: turning more users into paying customers. Revenue, engagement and onboarding completion are all important, but they only matter if they lead to this outcome.

**What to watch out for:** If we optimize only for conversion rate, we might attract lower-quality users who convert quickly but churn fast or generate refunds. That's why we also track revenue per converted user and refund rate as guardrails.

---

## KPI Tree Summary

The North Star (Paid Conversion Rate) breaks down into three main drivers:

**1. Acquisition Quality** : Are the right users even entering the funnel?
- Landing page visit rate
- Traffic source quality
- Device type mix

**2. Onboarding Effectiveness** : Do users actually get through the process?
- Trial start rate
- Onboarding completion rate
- Engagement score during onboarding

**3. Conversion Readiness** : Are users ready and willing to pay?
- Days to convert
- Plan type chosen
- Segment (region, device)

**Guardrail metrics** (things that should NOT get worse):
- Refund rate
- Support ticket rate
- Revenue per converted user

See `outputs/kpi_tree.png` for the full visual breakdown.

---

## What the Experiment Found

| Metric | Control | Treatment | Change |
|--------|---------|-----------|--------|
| Users | 693 | 715 | — |
| Landing Page Visit Rate | 63.6% | 72.6% | +9.0pp ↑ |
| Trial Start Rate | 25.1% | 29.1% | +4.0pp ↑ |
| Onboarding Completion Rate | 15.6% | 21.3% | +5.7pp ↑ |
| **Paid Conversion Rate** | **3.2%** | **7.0%** | **+3.8pp ↑** |
| Avg Revenue per User | ₹51.75 | ₹53.88 | +₹2.13 ↑ |
| Avg Revenue per Converted User | ₹1,630 | ₹770 | -₹860 ⚠ |
| Refund Rate | 0.0% | 0.4% | +0.4pp ⚠ |
| Support Ticket Rate | 0.219 | 0.372 | +0.153 ⚠ |
| Avg Engagement Score | 57.0 | 62.9 | +5.9 ↑ |
| Avg Days to Convert | 8.9 days | 6.4 days | -2.5 days ↑ |

---

## Hypothesis Test Result

We ran a one-tailed Z-test for proportions to check whether the conversion rate improvement is statistically significant or could have happened by chance.

- **Z-statistic:** 3.25
- **P-value:** 0.000573
- **Result:** Statistically significant at α = 0.05

The probability that this result happened by chance is less than 0.06%. We are very confident the campaign genuinely improved conversion rates. The null hypothesis (no improvement) is rejected.

---

## Guardrail Metric Analysis

This is the most important section for the launch decision.

**1. Refund Rate**
Control had zero refund requests. Treatment had 3 (0.4%). This is a small number, but the direction is concerning. It suggests a few users in Treatment converted but then changed their minds. Worth watching closely post-launch.

**2. Support Ticket Rate**
This is the most significant concern. Treatment users raised support tickets at an average rate of 0.372 vs 0.219 in Control -a **70% increase**. This is statistically significant (p < 0.001). The new campaign appears to be driving confusion or creating expectations that the product isn't meeting for some users. This increases operational costs and could hurt user satisfaction scores.

**3. Revenue per Converted User**
Treatment converted users generated ₹770 on average vs ₹1,630 in Control — a drop of 53%. This sounds alarming, but it may simply reflect that Treatment attracted more users on lower-value plans (Free users converting to Basic, for example) while Control had fewer but higher-value conversions. The overall revenue per user (across all users, not just converters) only differs by ₹2, which suggests the total revenue impact is small. Still, this should be tracked post-launch.

**4. Engagement Score**
Treatment users scored 62.9 vs 57.0 in Control -a meaningful improvement. This is a positive guardrail signal: users in Treatment are more engaged, which typically correlates with lower long-term churn.

**5. Days to Convert**
Treatment users converted 2.4 days faster on average (6.4 vs 8.9 days). This is good, faster conversion means less time for users to drop off.

---

## Segment-Level Insights

**By Region:**
The campaign worked across all regions, but North showed the strongest lift (+5.4pp). West showed the weakest response (+1.6pp), suggesting the campaign messaging may resonate differently depending on location.

**By Device:**
Mobile and Tablet users showed the largest gains (Treatment vs Control: +4.7pp and +5.3pp respectively). Desktop lift was smaller (+2.0pp). This suggests the new campaign experience may be particularly well-suited to mobile.

**By Plan Type:**
Free users in Treatment converted at 9.2% vs 3.1% in Control, a lift of +6.1pp. This is the standout segment. Basic plan users showed almost no improvement (+0.2pp), which is worth investigating.

---

## Final Recommendation

**Launch the campaign — but fix the support issue first.**

The conversion improvement is real, significant, and consistent across most segments. This is a strong result. However, the jump in support tickets needs to be understood before full rollout. Specifically:

1. **Investigate what's driving the support spike** — Are users confused about something in the new onboarding flow? Is there a specific step generating the most tickets?

2. **Add a short post-onboarding FAQ or tooltip** to address the most common questions proactively.

3. **Re-run a smaller experiment with the fix applied**, then launch if support tickets come down.

If fixing the support issue isn't feasible immediately, a **phased rollout** (e.g., 20% of new users first) would allow monitoring at scale before full launch.

---

## Risks and Limitations

- The revenue per converted user drop is unexplained and should be monitored. If it persists at scale, it could offset the conversion gains.
- The experiment had 8 duplicate user IDs which were flagged but not removed. These are a small share (< 1%) and unlikely to affect the results materially.
- Missing data in device_type (18 records) and traffic_source (24 records) means segment analysis is slightly incomplete.
- The experiment ran for one period — seasonal effects or novelty effects (users behaving differently simply because something is new) cannot be ruled out.

---

## Suggested Next Steps

1. Audit support tickets in the Treatment group to identify the root cause
2. Fix the friction point in the onboarding flow
3. Monitor refund rate weekly for 60 days post-launch
4. Run a follow-up segment test targeting Free and Mobile users specifically, where the lift was strongest
5. Set up automated alerts if support ticket rate exceeds 0.30 per user post-launch
