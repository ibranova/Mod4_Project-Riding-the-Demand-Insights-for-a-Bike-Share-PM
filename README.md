# Riding the Demand: Insights for a Bike-Share PM

## 📌 Business Framing and Stakeholders

This project analyzes hourly bike-share usage data to uncover demand patterns and generate actionable insights for key stakeholders:

* **Product Manager (PM):** Rider behavior, demand spikes, and priorities for future testing.
* **Operations Lead:** Staffing windows, rebalancing opportunities, and low-impact maintenance times.
* **Marketing Lead:** Promo timing and segmentation (casual vs. registered riders).
* **Policy & Ethics Advisor:** Ensure equity of access and responsible communication of uncertainty.

---

## 🔍 Methods Summary

* **Exploratory Data Analysis (EDA):**

  * Descriptive summaries, groupby analyses, and visualizations (time-series, boxplots, histograms, heatmaps).
* **Hypothesis Testing:**

  * **Q1:** Working vs. non-working days (Welch’s t-test).
  * **Q2:** Seasonal differences (One-way ANOVA + Tukey HSD post-hoc).
* **Simulated A/B Test:**

  * Stratified balancing across weekday × hour × weather.
  * Compared pre- vs. post-launch commuter-hour ridership.

---

## 📈 Top 3 Trends/Insights

1. **Seasonality Drives Demand:** Summer/fall peaks, winter lows → informs **Ops** staffing and maintenance planning.
2. **Commuter Peaks Dominate Weekdays:** 8–9 AM and 5–7 PM are the strongest demand windows → critical for **PM** feature design and **Marketing** targeting.
3. **Weather Sensitivity:** Clear/misty days with low humidity boost rides → enables **Marketing** to time promotions and **Ops** to anticipate sudden drops.

---

## 🧪 Hypothesis Testing Results

| Question                         | Test                      | α    | Test Statistic | p-value | 95% CI              | Decision  | Practical Significance        |
| -------------------------------- | ------------------------- | ---- | -------------- | ------- | ------------------- | --------- | ----------------------------- |
| Q1: Working vs. Non-working Days | Welch’s t-test            | 0.05 | t ≈ 5.2        | < 0.001 | [+20, +40] rides/hr | Reject H0 | +30 rides/hr → meaningful     |
| Q2: Seasonal Differences         | One-way ANOVA + Tukey HSD | 0.05 | F ≈ 50         | < 0.001 | N/A                 | Reject H0 | Confirms cyclical seasonality |

---

## 🧩 A/B Test Results (Commuter-Hour Focus)

* **Setup:** Pre (Aug 4–31, 2012) vs. Post (Sep 1–28, 2012), stratified by weekday × hour × weather.
* **Metric:** Average hourly rides (17–19h, working days, clear/misty weather, humidity ≤ 0.70).

| Group      | Mean Rides/hr | Sample Size         |
| ---------- | ------------- | ------------------- |
| Pre (Aug)  | ~100          | n = balanced sample |
| Post (Sep) | ~106          | n = balanced sample |

* **Test Result:**

  * t ≈ 1.9, p = 0.06
  * 95% CI: [−0.2, +12.4]
* **Decision:** Fail to reject H0.
* **Practical Significance:** +6 rides/hour (above +5 threshold) → meaningful but uncertain.
* **Recommendation:** Pilot with larger or randomized sample.

---

## ⚖️ Ethics & Limitations

* **Observational Data:** Results may be influenced by unobserved events (holidays, local disruptions).
* **Assumptions:** Normality/variance may not fully hold, though robust tests were used.
* **Equity Risks:** Over-focusing on commuter-heavy times could disadvantage casual/weekend riders. → Mitigation: Complement commuter strategies with leisure-focused campaigns.
* **Future Work:** Run randomized controlled pilots to strengthen causal claims and test equity impacts explicitly.
