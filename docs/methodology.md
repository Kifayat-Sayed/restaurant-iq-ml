# Methodology

## 1. Data Understanding

The project began with an exploratory examination of the restaurant dataset, including:

* Dataset dimensions
* Data types
* Missing values
* Duplicate records
* Unique categorical values
* Cuisine frequency
* Geographic coverage
* Rating distributions
* Pricing distributions

---

## 2. Data Preprocessing

Preprocessing was performed according to the requirements of each task.

The general workflow included:

```text
Raw Data
   ↓
Data Validation
   ↓
Missing-Value Handling
   ↓
Feature Selection
   ↓
Categorical Encoding
   ↓
Numerical Transformation
   ↓
Train/Test Split
   ↓
Model / Recommendation Pipeline
```

---

## 3. Task 1 Methodology

Restaurant rating prediction was formulated as a supervised regression problem.

The target variable was:

```text
Aggregate rating
```

Categorical variables were encoded and numerical variables were transformed where appropriate.

Model performance was evaluated using:

* Mean Absolute Error (MAE)
* Root Mean Squared Error (RMSE)
* R²
* Five-fold cross-validation

Permutation importance was used to investigate the contribution of individual features.

Additional error analysis was performed across rating ranges.

---

## 4. Task 2 Methodology

The recommendation system follows a content-based filtering approach.

Cuisine descriptions were transformed using TF-IDF.

The resulting vectors were compared using cosine similarity.

The recommendation pipeline can be represented as:

```text
User Cuisine Preference
          ↓
Cuisine Text Processing
          ↓
TF-IDF Representation
          ↓
Cosine Similarity
          ↓
Candidate Restaurants
          ↓
Rating / Price / Delivery Constraints
          ↓
Recommendation Score
          ↓
Top-N Recommendations
```

Hard constraints were evaluated separately from ranking scores.

This distinction ensures that a restaurant can be ranked highly while still being rejected if it violates a mandatory user requirement.

---

## 5. Task 3 Methodology

Cuisine prediction was formulated as a multi-label classification problem because a single restaurant may have multiple cuisine labels.

The original 146 cuisine categories were examined for frequency imbalance.

Labels with fewer than 20 occurrences were removed.

The resulting target contained 57 cuisine classes.

The target was represented using a binary indicator matrix:

```text
Restaurant × Cuisine
```

Model performance was evaluated using:

* Exact Match Accuracy
* Hamming Loss
* Micro Precision
* Micro Recall
* Micro F1
* Macro Precision
* Macro Recall
* Macro F1
* Weighted F1

Per-cuisine precision, recall, and F1 scores were also examined.

---

## 6. Task 4 Methodology

Location-based analysis examined the spatial and categorical distribution of restaurants.

The analysis included:

* Geographic completeness checks
* Latitude/longitude summary statistics
* Restaurant counts by city
* Restaurant counts by locality
* City-level rating statistics
* City-level vote statistics
* City-level price statistics

Cities and localities were ranked according to restaurant concentration.

---

## 7. Evaluation Philosophy

The project does not rely on a single performance metric.

Different tasks require different evaluation criteria:

| Task                   | Primary Evaluation                                  |
| ---------------------- | --------------------------------------------------- |
| Rating Prediction      | MAE, RMSE, R²                                       |
| Recommendation         | Constraint compliance, similarity, ranking quality  |
| Cuisine Classification | Micro/Macro/Weighted F1, precision, recall          |
| Location Analysis      | Descriptive statistics and geographic concentration |

This task-specific evaluation strategy provides a more appropriate assessment of the overall system.
