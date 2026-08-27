# 🍽️ RestaurantIQ

### End-to-End Machine Learning for Restaurant Intelligence

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://www.python.org/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange?logo=scikit-learn)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-purple?logo=pandas)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/NumPy-Scientific%20Computing-blue?logo=numpy)](https://numpy.org/)
[![Status](https://img.shields.io/badge/Project-Completed-success)]()

## 📌 Project Overview

**RestaurantIQ** is an end-to-end machine learning and data analytics project developed as part of the **Cognifyz Technologies Machine Learning Internship Program**.

The project explores restaurant data from multiple analytical perspectives, combining predictive modeling, recommendation systems, multi-label classification, and geographical analysis.

The implementation covers **three machine learning tasks and one analytical task**, exceeding the internship requirement of completing any three out of the four assigned tasks.

### Completed Tasks

| Task   | Project Component                | Status      |
| ------ | -------------------------------- | ----------- |
| Task 1 | Restaurant Rating Prediction     | ✅ Completed |
| Task 2 | Restaurant Recommendation System | ✅ Completed |
| Task 3 | Cuisine Classification           | ✅ Completed |
| Task 4 | Location-Based Analysis          | ✅ Completed |

---

# 🎯 Objectives

The project was designed to demonstrate practical application of machine learning and data science techniques to restaurant intelligence.

The major objectives were to:

* Predict restaurant aggregate ratings using supervised regression.
* Develop a content-based restaurant recommendation system.
* Classify restaurants across multiple cuisine categories.
* Analyze restaurant distribution geographically.
* Identify important factors influencing restaurant ratings.
* Evaluate model performance using appropriate statistical and machine learning metrics.
* Examine class imbalance and performance differences across cuisine categories.
* Translate analytical results into practical restaurant recommendations.

---

# 🏢 Internship Context

This project was completed as an original implementation for the **Cognifyz Technologies Machine Learning Internship Program**.

The internship provided a set of four restaurant-focused machine learning and data analytics tasks, of which participants were required to complete any three.

This repository documents the complete implementation of all four tasks.

The work presented here represents the author's own analysis, preprocessing decisions, model development, evaluation, recommendation logic, and interpretation.

> **Academic & Professional Integrity:** The implementation was developed as original work for the internship and is shared for educational and portfolio purposes.

---

# 📊 Dataset

The project uses a restaurant dataset containing information related to:

* Restaurant identity
* Location
* Cuisine
* Pricing
* Ratings
* Votes
* Online delivery
* Table booking
* Geographic coordinates

The working dataset contains approximately **9,551 restaurant records and 21 variables** before task-specific filtering and preprocessing.

For Task 3, cuisine-label filtering resulted in:

* **9,421 restaurants**
* **57 cuisine labels**
* **19,159 retained restaurant-cuisine assignments**
* **97.16% assignment retention**
* **98.64% restaurant retention**

---

# 🧠 Project Architecture

```text
                    Restaurant Dataset
                           │
                           ▼
                 Data Cleaning & EDA
                           │
              ┌────────────┼────────────┐
              │            │            │
              ▼            ▼            ▼
        Rating Model   Recommendation  Cuisine Model
              │            │            │
              ▼            ▼            ▼
        Regression     Content-Based   Multi-Label
        Evaluation     Ranking System   Classification
              │            │            │
              └────────────┼────────────┘
                           │
                           ▼
                  Location Analysis
                           │
                           ▼
                 Restaurant Intelligence
```

---

# 🔬 Task 1 — Restaurant Rating Prediction

## Objective

Predict the aggregate rating of a restaurant from available restaurant, location, pricing, and engagement features.

## Methodology

The workflow included:

1. Data cleaning and missing-value handling.
2. Feature preprocessing.
3. Encoding categorical variables.
4. Numerical feature transformation.
5. Train/test splitting.
6. Regression model training.
7. Cross-validation.
8. Permutation feature importance.
9. Rating-range error analysis.

## Model Evaluation

Five-fold cross-validation produced the following results:

| Metric |       Mean | Standard Deviation |
| ------ | ---------: | -----------------: |
| MAE    | **0.2545** |             0.0082 |
| RMSE   | **0.3463** |             0.0140 |
| R²     | **0.6063** |             0.0259 |

The model achieved an average absolute error of approximately **0.25 rating points**, while explaining approximately **60.6% of the variance** in restaurant ratings.

## Feature Importance

Permutation importance identified the following influential variables:

1. **Log Votes**
2. **Latitude**
3. **Longitude**
4. **Log Average Cost**
5. **Cuisines**
6. **Country Code**
7. **Currency**
8. **Has Online Delivery**
9. **Locality**
10. **City**

The dominance of vote count indicates that restaurant engagement/popularity contains substantial predictive information about aggregate ratings.

---

# 🍴 Task 2 — Restaurant Recommendation System

## Objective

Develop a content-based recommendation system that ranks restaurants according to user preferences.

## Recommendation Criteria

The system incorporates:

* Cuisine preference
* Restaurant rating
* Price range
* Average cost
* Online delivery availability
* Cuisine similarity

## Approach

Cuisine information was transformed using **TF-IDF vectorization**, producing a cuisine feature matrix of:

```text
9,551 restaurants × 152 TF-IDF features
```

Cosine similarity was then used to measure cuisine similarity between restaurants and user preferences.

A recommendation score was subsequently constructed by combining preference similarity with restaurant quality and compatibility factors.

## Example

For a **North Indian** preference, the system produced recommendations such as:

| Restaurant           | Cuisine                             | Rating | Cuisine Similarity | Recommendation Score |
| -------------------- | ----------------------------------- | -----: | -----------------: | -------------------: |
| Jai Vaishno Rasoi    | North Indian                        |    4.2 |              1.000 |                0.907 |
| The Culinary Pitaara | North Indian, Chinese               |    4.2 |              0.757 |                0.755 |
| Sagar Ratna          | South Indian, North Indian, Chinese |    4.0 |              0.650 |                0.701 |
| Dilli Treat          | North Indian, South Indian, Chinese |    4.2 |              0.650 |                0.701 |
| Dilli BC             | North Indian, Mughlai               |    4.4 |              0.624 |                0.686 |

## Recommendation Quality

The final hard-constraint evaluation achieved:

| Metric                       |     Result |
| ---------------------------- | ---------: |
| Recommendations Generated    |         10 |
| Cuisine Relevance            |   **100%** |
| Rating Compliance            |   **100%** |
| Delivery Compliance          |   **100%** |
| Hard Constraint Satisfaction |   **100%** |
| Mean Price Compatibility     | **76.67%** |

The recommendation system therefore successfully enforced the defined hard constraints while ranking candidates according to preference compatibility.

---

# 🌍 Task 3 — Cuisine Classification

## Objective

Develop a machine learning system capable of predicting multiple cuisine labels for restaurants.

Unlike conventional single-class classification, restaurants may belong to multiple cuisine categories. Therefore, the task was formulated as a **multi-label classification problem**.

## Dataset Preparation

The original dataset contained:

* 146 unique cuisine labels
* 19,719 restaurant-cuisine assignments

To reduce extreme sparsity and improve the reliability of evaluation, cuisines occurring fewer than 20 times were removed.

The resulting dataset contained:

* **57 cuisine labels**
* **9,421 restaurants**
* **19,159 retained cuisine assignments**

This retained **97.16% of all cuisine-label assignments**.

## Feature Matrix

The model used:

### Numerical Features

* Longitude
* Latitude
* Average Cost for two
* Price range
* Aggregate rating
* Votes

### Categorical Features

* Country Code
* City
* Locality
* Currency
* Has Table booking
* Has Online delivery
* Is delivering now
* Switch to order menu

The target variable was the multi-label cuisine matrix.

## Evaluation

| Metric               |      Score |
| -------------------- | ---------: |
| Exact Match Accuracy |     0.0021 |
| Hamming Loss         |     0.1336 |
| Micro Precision      |     0.1548 |
| Micro Recall         |     0.6211 |
| Micro F1             |     0.2478 |
| Macro Precision      |     0.1033 |
| Macro Recall         |     0.4852 |
| Macro F1             |     0.1598 |
| Weighted F1          | **0.3524** |

## Best Performing Cuisine

The strongest performance was observed for **North Indian**:

* Support: 817
* Precision: 0.564
* Recall: 0.678
* F1: **0.616**

Other relatively strong classes included Chinese, Fast Food, Continental, Italian, and American.

## Classification Challenges

The results demonstrate substantial class imbalance.

Several low-frequency cuisines achieved very low or zero F1 scores because the model had insufficient examples to learn reliable class-specific patterns.

This illustrates an important limitation of the dataset: **rare cuisine categories are substantially more difficult to classify than frequent cuisines**.

---

# 📍 Task 4 — Location-Based Analysis

## Objective

Analyze the geographical distribution and concentration of restaurants.

## Geographic Coverage

The dataset contained:

* **141 unique cities**
* **1,208 unique localities**
* No missing city values
* No missing locality values
* No missing latitude values
* No missing longitude values

## Restaurant Concentration

The largest restaurant concentrations were observed in:

| City      | Restaurant Count |
| --------- | ---------------: |
| New Delhi |            5,473 |
| Gurgaon   |            1,118 |
| Noida     |            1,080 |
| Faridabad |              251 |
| Ghaziabad |               25 |

New Delhi therefore represents the dominant geographic concentration in the dataset.

## Locality Concentration

The highest-density localities included:

* Connaught Place
* Rajouri Garden
* Shahdara
* Defence Colony
* Malviya Nagar
* Pitampura
* Mayur Vihar Phase 1
* Rajinder Nagar
* Safdarjung
* Satyaniketan

## City-Level Insights

The analysis also revealed substantial differences in average restaurant ratings, votes, and price ranges between cities.

For example:

* New Delhi: average rating ≈ **2.44**
* Gurgaon: average rating ≈ **2.65**
* Noida: average rating ≈ **2.04**
* Lucknow: average rating ≈ **4.20**
* Abu Dhabi: average rating ≈ **4.30**

However, cities with very small restaurant counts should be interpreted cautiously because their statistics are more sensitive to sampling variation.

---

# 📈 Key Findings

Several important findings emerged from the project.

### 1. Restaurant engagement is highly informative

Log-transformed vote count was the most influential feature in the rating prediction model.

### 2. Geographic information contributes predictive signal

Latitude, longitude, locality, and city contributed to rating prediction, suggesting that restaurant ratings vary geographically.

### 3. Content-based recommendation can effectively enforce preferences

The recommendation system achieved **100% compliance with its defined hard constraints** for the evaluated recommendation set.

### 4. Cuisine classification is strongly affected by imbalance

Frequent cuisines such as North Indian and Chinese were substantially easier to classify than rare cuisines.

### 5. Restaurant distribution is highly concentrated

A large proportion of the dataset is concentrated in New Delhi, Gurgaon, and Noida.

### 6. Price and quality are not uniformly distributed geographically

Average price range and restaurant ratings vary considerably across cities.

---

# ⚠️ Limitations

The project also has several important limitations.

### Rating Prediction

The rating model relies heavily on vote count, which may reflect restaurant popularity and engagement rather than intrinsic food quality.

### Recommendation System

The recommendation engine is content-based and does not learn collaborative user behavior. It therefore cannot capture user-to-user preference patterns.

### Cuisine Classification

The multi-label classification task suffers from severe class imbalance, particularly among rare cuisines.

### Location Analysis

Some cities contain very few observations. Comparisons involving such cities should therefore be treated as descriptive rather than statistically conclusive.

### Dataset Representation

The dataset does not necessarily represent the global restaurant industry uniformly because restaurant coverage varies considerably by location.

---

# 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Scikit-learn
* Matplotlib
* Seaborn
* Jupyter Notebook
* TF-IDF Vectorization
* Cosine Similarity
* Machine Learning Regression
* Multi-Label Classification
* Statistical Analysis
* Exploratory Data Analysis

---

# 📁 Repository Structure

```text
restaurant-iq-ml/
│
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
│
├── data/
├── notebooks/
├── src/
├── models/
├── reports/
├── docs/
└── presentation/
```

---

# 🚀 How to Run

## 1. Clone the repository

```bash
git clone https://github.com/<your-username>/restaurant-iq-ml.git
cd restaurant-iq-ml
```

## 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it:

### Windows

```bash
.venv\Scripts\activate
```

### macOS/Linux

```bash
source .venv/bin/activate
```

## 3. Install dependencies

```bash
pip install -r requirements.txt
```

## 4. Launch Jupyter

```bash
jupyter notebook
```

Open the notebooks in the `notebooks/` directory.

---

# 📚 Documentation

Additional documentation is available in:


# 🎓 Internship

**Program:** Machine Learning Internship
**Organization:** Cognifyz Technologies
**Project:** RestaurantIQ
**Domain:** Machine Learning / Data Science
**Tasks Completed:** 4 / 4

This repository serves as a technical portfolio and documentation of the work completed during the internship.

---

# 📜 License

This project is intended primarily for educational and portfolio purposes.

Refer to the repository license for permitted use and redistribution.

---

# 👤 Author

*Kifayat Sayed**

M.Sc. Artificial Intelligence & Machine Learning / Data Science


LinkedIn: [https://in.linkedin.com/in/kifayat-sayed]

---

## ⭐ Acknowledgement

I would like to acknowledge **Cognifyz Technologies** for providing the Machine Learning Internship opportunity and the restaurant analytics problem statements used as the basis for this project.

---

**RestaurantIQ — Turning Restaurant Data into Machine Learning Insights.**
