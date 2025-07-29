# Quasi-experiment
Effectiveness of two customer acquisition promotions

*   **Promotion 1:** 7% bonus on the first purchase for "New" customers (no purchases in the last 6+ months).
*   **Promotion 2:** 6% bonus on the first purchase for "Churn" customers (no purchases in the last 3-6 months, but had prior purchases).

For each promotion, a target group (receiving communication about the promotion) and a control group (no communication) were prepared. The goal is to evaluate the promotions' impact on customer behavior and calculate any additional revenue generated for the partner.

## Key Challenge: Severe Group Imbalance

A critical issue identified in the provided data is a **significant imbalance** between the test and control groups:

*   **7% "New":** ~13,378 in test vs. ~1,474 in control (**~80.2% imbalance**).
*   **6% "Churn":** ~3,545 in test vs. ~342 in control (**~82.4% imbalance**).

This severe imbalance poses a significant challenge for standard A/B testing methodologies, leading to **very low statistical power** and making it difficult to reliably detect true effects.

## Methodology

1.  **Data Preparation:** Transaction data was cleaned, first purchases were identified, and groups were validated for overlaps.
2.  **Metric Calculation:** Key client-level metrics were calculated for each group:
    *   Average Check (`avg_check`)
    *   Transaction Count (`transaction_count`)
    *   Repeat Purchase Rate (`has_repeat_purchase`)
    *   Total Revenue (`total_revenue`)
    *   Total Bonus Awarded (`total_bonus`)
    *   Additional Cost to Partner (`additional_cost`)
3.  **Statistical Analysis (Quasi-Experiment):** Due to group imbalance, a **Bootstrap analysis with sample balancing** was employed. This method resamples the data to create balanced groups (matching the size of the smaller group) and calculates confidence intervals and p-values for the difference in means of key metrics.
4.  **Power Analysis:** The statistical power of the tests was calculated post-analysis to understand the reliability of the results.

## Results Summary

### Statistical Analysis (Bootstrap with Balancing)

No statistically significant differences (p > 0.05) were found between the test and control groups for the key **behavioral metrics** after balancing.

**7% "New" Promotion (Balanced group size: 1,474):**

| Metric               | Observed Diff | 95% CI              | p-value |
| :------------------- | :------------ | :------------------ | :------ |
| `avg_check`          | +41.05        | [-24.29, 106.65]    | 0.516   |
| `transaction_count`  | +0.01         | [-0.03, 0.05]       | 0.587   |
| `has_repeat_purchase`| +0.01         | [-0.02, 0.04]       | 0.558   |
| `total_revenue`      | +40.00        | [-22.35, 101.04]    | 0.508   |

**6% "Churn" Promotion (Balanced group size: 342):**

| Metric               | Observed Diff | 95% CI               | p-value |
| :------------------- | :------------ | :------------------- | :------ |
| `avg_check`          | +36.99        | [-108.13, 308.47]    | 0.604   |
| `transaction_count`  | +0.04         | [-0.06, 0.14]        | 0.575   |
| `has_repeat_purchase`| +0.02         | [-0.04, 0.08]        | 0.654   |
| `total_revenue`      | +21.02        | [-126.97, 287.34]    | 0.765   |

*(Note: `total_bonus` and `additional_cost` showed differences as expected due to the promotion mechanics, but these are not primary indicators of customer behavioral change.)*

### Power Analysis

The statistical power of the tests is critically low due to the group imbalance:

*   **7% "New" Promotion:** Power for behavioral metrics ranges from **~15.6% to ~41.8%**.
*   **6% "Churn" Promotion:** Power for behavioral metrics ranges from **~6.0% to ~17.8%**.

**Implication:** A low power test has a high probability of **failing to detect a real effect** if one exists.

## Conclusion

Based on the analysis:

*   **No statistically significant evidence** of a behavioral impact from either the 7% "New" or 6% "Churn" promotions was found.
*   However, this conclusion is **heavily constrained by the extremely low statistical power** resulting from the severe imbalance in group sizes.
*   Therefore, it is **not possible to reliably confirm or deny** the effectiveness of the promotions using the current data structure.

## Recommendations

1.  **For Future Promotions:** Ensure that **control groups are significantly larger** (ideally 30-50% the size of the test group) to allow for robust statistical analysis.
2.  **For Current Data:** Acknowledge the limitations. Any conclusions about effectiveness are unreliable due to the low-powered test design.
