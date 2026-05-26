# Mall Customer Segmentation using K-Means Clustering

## Problem Statement

Retail businesses often struggle to understand the diversity within their customer base. Treating all customers the same leads to ineffective marketing, missed revenue opportunities, and poor customer experience. This project addresses the challenge of **identifying distinct customer segments** based on their annual income and spending behavior, enabling targeted marketing strategies and personalized offerings for each group.

The goal is to answer: *Which groups of customers share similar financial and spending profiles, and how can a mall tailor its services and promotions to each group?*

---

## Dataset Details

**Dataset:** Mall Customers Dataset (`Mall_Customers.csv`)

| Feature | Description |
|---|---|
| `CustomerID` | Unique identifier for each customer |
| `Gender` | Customer gender (Male / Female) |
| `Age` | Customer age in years |
| `Annual Income (k$)` | Annual income in thousands of dollars |
| `Spending Score (1-100)` | Score assigned by the mall based on customer behavior and purchasing data (1 = low spender, 100 = high spender) |

- **Source:** Commonly used benchmark dataset for clustering tasks (available on Kaggle)
- **Size:** 200 customer records
- **Missing Values:** None

---

## Approach

### 1. Data Loading & Exploration
The dataset was loaded using `pandas`. Initial exploration included inspecting the first few rows, checking for null values, and reviewing data types and distributions.

### 2. Feature Selection
Two features were selected for clustering:
- `Annual Income (k$)`
- `Spending Score (1-100)`

These two features capture both the financial capacity and the actual spending behavior of customers — the most relevant dimensions for customer segmentation.

### 3. Feature Scaling
Features were standardized using `StandardScaler` (zero mean, unit variance) to ensure neither feature dominates the distance calculations in K-Means.

### 4. Determining Optimal K — Elbow Method
K-Means was run for K = 1 through 10. The Within-Cluster Sum of Squares (WCSS) was plotted against K. The "elbow" in the curve — where WCSS begins to decrease more slowly — indicated the optimal number of clusters.

**Optimal K selected: 5**

### 5. K-Means Clustering
K-Means was applied with:
- `n_clusters = 5`
- `init = 'k-means++'` (smart centroid initialization to avoid poor local minima)
- `random_state = 42` (reproducibility)
- `n_init = 10`

Cluster labels were appended to the original DataFrame.

### 6. Visualization
A scatter plot was generated using `seaborn`, with each cluster color-coded, to visualize the separation between customer segments across the income–spending space.

---

## Results

Five distinct customer segments were identified:

| Cluster | Annual Income | Spending Score | Profile |
|---|---|---|---|
| 0 | High | Low | High earners who spend conservatively — potential targets for premium loyalty programs |
| 1 | Low | High | Low earners who spend heavily — price-sensitive but engaged; respond well to deals |
| 2 | Medium | Medium | Average customers across both dimensions — the general majority |
| 3 | High | High | High earners who spend freely — the most valuable segment; targets for luxury offerings |
| 4 | Low | Low | Low earners who spend minimally — limited engagement; budget-focused |

> *Exact cluster label numbers may vary by run; the profiles above reflect the behavioral archetypes identified.*

### Key Takeaways
- The Elbow Method clearly suggested **K = 5** as the optimal number of clusters.
- K-Means++ initialization produced well-separated, interpretable clusters.
- The **high-income / high-spending** segment represents the mall's most profitable customers and warrants dedicated retention and upsell strategies.
- The **low-income / high-spending** segment signals strong brand loyalty despite financial constraints, making them ideal candidates for reward programs and discounts.

---

## Tech Stack

- **Python 3**
- `pandas` — data loading and manipulation
- `scikit-learn` — feature scaling (`StandardScaler`) and clustering (`KMeans`)
- `matplotlib` — Elbow Method visualization
- `seaborn` — cluster scatter plot
