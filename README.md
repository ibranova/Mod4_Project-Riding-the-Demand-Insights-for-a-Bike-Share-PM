# Riding the Demand: Insights for a Bike-Share PM

## Business Framing and Stakeholders

This project analyzes hourly bike-share usage data to uncover demand patterns and generate actionable insights for key stakeholders:

* **Product Manager (PM):** Rider behavior, demand spikes, and priorities for future testing.
* **Operations Lead:** Staffing windows, rebalancing opportunities, and low-impact maintenance times.
* **Marketing Lead:** Promo timing and segmentation (casual vs. registered riders).
* **Policy & Ethics Advisor:** Ensure equity of access and responsible communication of uncertainty.

---

## Methods Summary

* **Exploratory Data Analysis (EDA):**

  * Imported the data using the pandas library in Python, checked for missing and duplicated values, and then performed data cleaning and feature engineering for some columns to better understand the data. For example, instead of having months in numbers starting from 0-12, I created a dictionary named Month_name in Python to map each number to its corresponding month. Next, I explored hourly ridership across time, season, weather, and user segments. Used descriptive statistics and visualizations (time-series plots, boxplots, histograms, heatmaps).
* **Hypothesis Testing:**

  * **Q1:** Compared average hourly rides between working vs. non-working days
     * For this hypothesis, I chose a Welch’s t-test because the data are independent and approximately normally distributed. Also, the sample is large, and we are comparing the means of two groups. (a.k.a. pairwise comparison).
  * **Q2:** Tested if mean hourly rides differ across seasons.
     * I used a `one-way ANOVA with post-hoc Tukey HSD` to perform this test because we are analyzing the difference between the means of more than 2 samples.
* **Simulated A/B Test:**

  * Measured the impact of a feature launch on early evening commuter-hour ridership. Designed with stratified balancing across weekday × hour × weather
  * Compared pre- vs. post-launch commuter-hour ridership.

---

## Top 3 Trends/Insights

1. **Seasonal Demand is Strongly Cyclical:** Summer and fall show peak ridership, while winter dips significantly. It helps Ops plan maintenance in low-demand months.
   ![Average ride by season](avg_rides_by_season.png)
3. **Commuter Peaks Dominate Weekdays:** 8–9 AM and 5–7 PM are the highest ridership windows, especially for registered riders. This is critical for PM/Ops planning and Marketing targeting.
4. **Weather & Humidity Drive Demand:** Clear or misty days with humidity ≤ 70% see much higher ridership, while rain and snow sharply reduce usage. → Enables Marketing to time promos and Ops to anticipate sudden drops.
---

## Hypothesis Testing Results

| Question                         | Test                      | α    | Test Statistic | p-value | 95% CI              | Decision  | Practical Significance        |
| -------------------------------- | ------------------------- | ---- | -------------- | ------- | ------------------- | --------- | ----------------------------- |
| Q1: Working vs. Non-working Days | Welch’s t-test            | 0.05 | t ≈ 5.2        | < 0.001 | [+20, +40] rides/hr | Reject H0 | +30 rides/hr → meaningful     |
| Q2: Seasonal Differences         | One-way ANOVA + Tukey HSD | 0.05 | F ≈ 50         | < 0.001 | N/A                 | Reject H0 | Confirms cyclical seasonality |

---

## A/B Test Results (Commuter-Hour Focus)

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
* **Recommendation:** Pilot with a larger or randomized sample.

---

## ⚖️ Ethics & Limitations

* **Observational Data:** Results may be influenced by unobserved events (holidays, local disruptions).
* **Assumptions:** Normality/variance may not fully hold, though robust tests were used.
* **Equity Risks:** Over-focusing on commuter-heavy times could disadvantage casual/weekend riders. → Mitigation: Complement commuter strategies with leisure-focused campaigns.
* **Future Work:** Run randomized controlled pilots to strengthen causal claims and test equity impacts explicitly.
