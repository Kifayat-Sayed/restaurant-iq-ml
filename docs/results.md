# Results Summary

## Task 1 — Rating Prediction

Five-fold cross-validation:

| Metric |   Mean |    Std |
| ------ | -----: | -----: |
| MAE    | 0.2545 | 0.0082 |
| RMSE   | 0.3463 | 0.0140 |
| R²     | 0.6063 | 0.0259 |

The model achieved stable performance across the five folds, with relatively low variation in MAE.

The most influential feature was **Log Votes**, followed by geographic variables including latitude and longitude.

---

## Task 2 — Recommendation

The recommendation system generated 10 recommendations for the evaluated user preference.

| Metric                       | Result |
| ---------------------------- | -----: |
| Recommendations Generated    |     10 |
| Cuisine Relevance            |   100% |
| Rating Compliance            |   100% |
| Delivery Compliance          |   100% |
| Hard Constraint Satisfaction |   100% |
| Mean Price Compatibility     | 76.67% |

The results demonstrate successful enforcement of mandatory recommendation criteria.

---

## Task 3 — Cuisine Classification

| Metric               | Result |
| -------------------- | -----: |
| Exact Match Accuracy | 0.0021 |
| Hamming Loss         | 0.1336 |
| Micro Precision      | 0.1548 |
| Micro Recall         | 0.6211 |
| Micro F1             | 0.2478 |
| Macro Precision      | 0.1033 |
| Macro Recall         | 0.4852 |
| Macro F1             | 0.1598 |
| Weighted F1          | 0.3524 |

North Indian was the strongest high-support cuisine class with an F1 score of approximately **0.616**.

The major limitation was class imbalance, particularly among rare cuisine categories.

---

## Task 4 — Location Analysis

The dataset contains:

* 141 cities
* 1,208 localities
* 9,551 restaurants

The largest concentration occurs in New Delhi, followed by Gurgaon and Noida.

The geographic analysis also revealed substantial variation in restaurant ratings, votes, and price levels across cities.

---

## Overall Interpretation

The project demonstrates that restaurant data can support several complementary machine learning applications.

The strongest predictive result was obtained in rating prediction, while the recommendation system demonstrated excellent compliance with predefined hard constraints.

Cuisine classification remains the most challenging machine learning component because of the multi-label nature of the problem and severe class imbalance.

The location analysis provides additional contextual information that can help explain differences in restaurant density, ratings, popularity, and pricing.
