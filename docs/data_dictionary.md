# Data Dictionary

## Overview

The restaurant dataset contains restaurant-level information covering identity, location, cuisine, pricing, customer engagement, ratings, and service availability.

The original working dataset contains **9,551 restaurant records and 21 columns**.

---

## Variables

| Variable             | Type                    | Description                                       | Role                                  |
| -------------------- | ----------------------- | ------------------------------------------------- | ------------------------------------- |
| Restaurant ID        | Integer                 | Unique identifier assigned to a restaurant        | Identifier                            |
| Restaurant Name      | String                  | Name of the restaurant                            | Descriptive                           |
| Country Code         | Integer                 | Numeric country identifier                        | Feature                               |
| City                 | Categorical             | City in which the restaurant is located           | Feature                               |
| Address              | String                  | Restaurant address                                | Descriptive                           |
| Locality             | Categorical             | Local area/neighborhood                           | Feature                               |
| Locality Verbose     | String                  | Detailed locality description                     | Descriptive                           |
| Longitude            | Numeric                 | Geographic longitude                              | Feature                               |
| Latitude             | Numeric                 | Geographic latitude                               | Feature                               |
| Cuisines             | Multi-label categorical | Cuisine categories associated with the restaurant | Target / Feature depending on task    |
| Average Cost for two | Numeric                 | Average cost for two people                       | Feature                               |
| Currency             | Categorical             | Currency used for the average cost                | Feature                               |
| Has Table booking    | Binary                  | Whether table booking is available                | Feature                               |
| Has Online delivery  | Binary                  | Whether online delivery is available              | Feature                               |
| Is delivering now    | Binary                  | Whether the restaurant is currently delivering    | Feature                               |
| Switch to order menu | Binary                  | Availability of an order-menu option              | Feature                               |
| Price range          | Ordinal                 | Restaurant price category                         | Feature                               |
| Aggregate rating     | Numeric                 | Overall restaurant rating                         | Target for Task 1 / Feature elsewhere |
| Rating color         | Categorical             | Color category associated with the rating         | Descriptive                           |
| Rating text          | Categorical             | Textual category associated with the rating       | Descriptive                           |
| Votes                | Integer                 | Number of votes received by the restaurant        | Feature                               |

---

## Task-Specific Roles

### Task 1 — Rating Prediction

**Target:**

```text
Aggregate rating
```

Features include restaurant location, pricing, cuisine, service availability, and engagement variables.

### Task 2 — Recommendation

The recommendation system uses:

* Cuisines
* Aggregate rating
* Price range
* Average Cost for two
* Votes
* Online delivery
* Table booking
* Geographic/location information

### Task 3 — Cuisine Classification

**Target:**

```text
Cuisines
```

The cuisine field is transformed into a multi-label binary target matrix.

After frequency filtering:

```text
Restaurants: 9,421
Cuisine labels: 57
Target matrix: 9,421 × 57
```

### Task 4 — Location Analysis

Primary geographic variables:

```text
City
Locality
Latitude
Longitude
```

Additional analytical variables:

```text
Aggregate rating
Votes
Price range
Average Cost for two
Cuisines
```

---

## Data Quality Notes

The original cuisine field contained **9 missing values**.

The original dataset contained **146 unique cuisine labels**.

Cuisine frequency was highly skewed, with several cuisines occurring only a handful of times.

For Task 3, cuisine labels occurring fewer than 20 times were excluded to reduce extreme sparsity.

This resulted in:

* 57 retained cuisine labels
* 9,421 restaurants
* 19,159 retained cuisine assignments

The filtering retained:

**97.16% of restaurant-cuisine assignments**

and

**98.64% of restaurants.**

---

## Important Interpretation Notes

### Aggregate Rating

The aggregate rating represents the restaurant's recorded overall rating in the dataset. It should not automatically be interpreted as an objective measure of food quality.

### Votes

Votes represent customer engagement and can also act as a proxy for restaurant popularity or visibility.

### Price Range

Price range is an ordinal category rather than a continuous monetary measurement.

### Cuisine

A restaurant can belong to multiple cuisine categories. Therefore, cuisine prediction is treated as a **multi-label classification problem** rather than conventional single-class classification.
