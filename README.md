# Mall Customer Segmentation

## Unsupervised Learning — Practical Report 1

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-F7931E)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## Project Overview

This project is based on **Unsupervised Learning** and focuses on customer segmentation using the **Mall Customer Segmentation Dataset**.

The objective is to identify groups of customers with similar characteristics and spending behaviour using clustering algorithms.

The project implements and compares the following algorithms:

- K-Means Clustering
- Agglomerative Hierarchical Clustering
- DBSCAN Clustering

The complete project includes:

- Dataset loading
- Dataset inspection
- Data preprocessing
- Exploratory Data Analysis
- Feature encoding
- Feature scaling
- Feature selection
- K-Means clustering
- Agglomerative Hierarchical Clustering
- DBSCAN clustering
- Cluster evaluation
- Algorithm comparison
- Customer segmentation
- Business insights

---

## Academic Information

| Field | Details |
|---|---|
| Institute | Red & White Skill Education |
| Subject | Unsupervised Learning |
| Project | Practical Report 1 (PR 1) |
| Dataset | Mall Customer Segmentation Dataset |
| Domain | Retail / Customer Analytics |
| Algorithms | K-Means, Agglomerative Hierarchical, DBSCAN |
| Total Marks | 10 |

---

## Objectives

The main objectives of this project are:

1. Load and inspect the Mall Customer dataset.
2. Perform exploratory data analysis.
3. Check missing values and duplicate records.
4. Remove the `CustomerID` identifier.
5. Rename the required columns.
6. Encode the `Gender` column.
7. Apply `StandardScaler` to numerical features.
8. Create the two-feature clustering dataset.
9. Determine the optimal number of K-Means clusters.
10. Implement Agglomerative Hierarchical Clustering.
11. Tune and implement DBSCAN.
12. Compare the three clustering algorithms.
13. Evaluate clustering performance.
14. Identify meaningful customer segments.
15. Generate business insights and marketing strategies.

---

# Dataset

## Dataset Name

**Mall Customer Segmentation Dataset**

## Dataset Source

The dataset is sourced from Kaggle:

https://www.kaggle.com/datasets/vjchoudhary7/customer-segmentation-tutorial-in-python

## Dataset File

```text
Mall_Customers.csv
```

## Dataset Size

```text
Rows    : 200
Columns : 5
```

## Dataset Quality

```text
Missing Values : 0
Duplicate Rows : 0
```

---

## Original Dataset Columns

| Column | Description |
|---|---|
| `CustomerID` | Unique customer identifier |
| `Gender` | Customer gender |
| `Age` | Customer age |
| `Annual Income (k$)` | Estimated annual income in thousands of USD |
| `Spending Score (1-100)` | Mall-assigned spending score |

---

# Data Preprocessing

The following preprocessing steps were performed before clustering.

## 1. Remove CustomerID

`CustomerID` is a unique identifier and does not represent customer behaviour.

Therefore, it was removed before clustering.

## 2. Rename Columns

The following columns were renamed:

```text
Annual Income (k$)       -> Annual_Income
Spending Score (1-100)   -> Spending_Score
```

## 3. Encode Gender

The `Gender` column was converted into numerical form using `LabelEncoder`.

```text
Female -> 0
Male   -> 1
```

## 4. Feature Scaling

`StandardScaler` was applied to:

```text
Age
Annual_Income
Spending_Score
```

`Gender` was not scaled because it was already represented as a binary value.

## 5. Feature Selection

The primary clustering dataset was created using:

```text
Annual_Income
Spending_Score
```

These two features were selected because they provide a clear two-dimensional representation of customer income and spending behaviour.

---

# Exploratory Data Analysis

The following EDA operations were performed:

- Dataset inspection
- `head()`
- `info()`
- `describe()`
- Missing-value analysis
- Duplicate-value analysis
- Age distribution
- Annual Income distribution
- Spending Score distribution
- Pairplot
- Correlation heatmap

---

## EDA Findings

The analysis showed:

- The dataset contains 200 customer records.
- The dataset contains no missing values.
- The dataset contains no duplicate records.
- Age and Spending Score have a moderate negative relationship.
- Annual Income and Spending Score have very little linear correlation.
- Annual Income and Spending Score provide a useful two-dimensional space for customer segmentation.
- The pairplot shows visible customer groupings.

---

# K-Means Clustering

## Elbow Method

K-Means was tested for:

```text
k = 1 to 10
```

The Elbow Method was used to examine the reduction in within-cluster inertia as the number of clusters increased.

The analysis indicated that approximately **5 clusters** provided a suitable balance between cluster compactness and model complexity.

## Silhouette Score

Silhouette Scores were calculated for:

```text
k = 2 to 10
```

The highest Silhouette Score occurred at:

```text
k = 5
```

Approximate Silhouette Score:

```text
0.555
```

## Final K-Means Configuration

```python
KMeans(
    n_clusters=5,
    random_state=42,
    n_init=10
)
```

---

# Agglomerative Hierarchical Clustering

Agglomerative Hierarchical Clustering was implemented using **Ward linkage**.

## Configuration

```text
Linkage        : Ward
Number Clusters: 5
```

A dendrogram was created to visualize the hierarchical relationships between customers.

The hierarchical clustering result was compared with the K-Means clustering result.

---

# DBSCAN Clustering

DBSCAN was implemented as a density-based clustering algorithm.

## Parameter Tuning

The following `eps` values were tested:

```text
0.2
0.3
0.4
0.5
0.6
```

The following `min_samples` values were tested:

```text
3
4
5
6
```

A 4-nearest-neighbour distance plot was also generated to assist with selecting the `eps` parameter.

## Selected Parameters

```text
eps = 0.4
min_samples = 3
```

## DBSCAN Result

```text
Number of Clusters = 4
Noise Points       = 10
```

DBSCAN assigns the label `-1` to observations classified as noise.

---

# Model Evaluation

The clustering algorithms were evaluated using:

- Silhouette Score
- Davies-Bouldin Index
- Calinski-Harabasz Index

## Evaluation Results

| Algorithm | Number of Clusters | Silhouette Score | Davies-Bouldin Index | Calinski-Harabasz Index |
|---|---:|---:|---:|---:|
| K-Means | 5 | 0.555 | 0.572 | 248.649 |
| Hierarchical | 5 | 0.554 | 0.578 | 244.410 |
| DBSCAN | 4 | 0.395 | 0.601 | 97.172 |

> For DBSCAN, noise observations were excluded from the clustering metric calculations.

---

# Customer Segmentation

The K-Means model produced five interpretable customer segments.

## Cluster 0 — Moderate Income / Moderate Spenders

These customers have moderate annual income and moderate spending behaviour.

### Marketing Strategy

- General promotions
- Membership benefits
- Personalized offers
- Cross-selling campaigns

---

## Cluster 1 — High Income / High Spenders

These customers have high annual income and high spending scores.

### Marketing Strategy

- VIP loyalty programs
- Premium products
- Exclusive offers
- Personalized rewards
- Early-access campaigns

---

## Cluster 2 — Low Income / High Spenders

These customers have relatively low income but high spending scores.

### Marketing Strategy

- Discounts
- Product bundles
- Promotional campaigns
- Affordable premium products

---

## Cluster 3 — High Income / Low Spenders

These customers have high income but comparatively low spending scores.

### Marketing Strategy

- Personalized recommendations
- Premium product demonstrations
- Purchase incentives
- Loyalty campaigns
- Targeted offers

---

## Cluster 4 — Low Income / Low Spenders

These customers have relatively low income and low spending scores.

### Marketing Strategy

- Budget-friendly products
- Discounts
- Value bundles
- Entry-level loyalty rewards

---

# Business Insights

Customer segmentation allows the mall to use different marketing strategies for different customer groups.

## High Income + High Spending

Recommended focus:

- Premium products
- VIP programs
- Exclusive rewards
- Personalized experiences

## Low Income + High Spending

Recommended focus:

- Discounts
- Product bundles
- Promotional campaigns
- Affordable premium products

## High Income + Low Spending

Recommended focus:

- Personalized recommendations
- Purchase incentives
- Premium demonstrations
- Loyalty campaigns

## Low Income + Low Spending

Recommended focus:

- Budget products
- Value offers
- Discounts
- Entry-level rewards

## Moderate Income + Moderate Spending

Recommended focus:

- Cross-selling
- Personalized offers
- Membership benefits
- Customer engagement

---

# Algorithm Comparison

## K-Means

K-Means is a centroid-based clustering algorithm.

### Advantages

- Simple to understand
- Easy to implement
- Fast
- Easy to visualize
- Produces interpretable customer segments

### Limitation

The number of clusters must be selected before fitting the final model.

---

## Agglomerative Hierarchical Clustering

Hierarchical clustering builds a hierarchy of customer observations.

### Advantages

- Provides hierarchical relationships
- Dendrogram gives a visual representation of cluster structure
- Useful for management presentations
- Can help understand how groups are progressively merged

### Limitation

The interpretation can be more complex than K-Means when the objective is simply to create directly usable customer segments.

---

## DBSCAN

DBSCAN is a density-based clustering algorithm.

### Advantages

- Does not require the number of clusters to be specified beforehand
- Can identify dense regions
- Can detect noise observations
- Can identify non-spherical cluster structures

### Limitation

The result is sensitive to `eps` and `min_samples`.

---

# Final Conclusion

The project successfully implemented three major unsupervised learning algorithms for Mall Customer Segmentation.

The dataset was first inspected and cleaned. `CustomerID` was removed, the required columns were renamed, Gender was encoded, and the numerical features were standardized.

Annual Income and Spending Score were selected as the primary clustering features because they provide an interpretable two-dimensional representation of customer behaviour.

K-Means clustering identified five customer segments. Both the Elbow Method and Silhouette Score supported a five-cluster solution.

Agglomerative Hierarchical Clustering also produced five meaningful groups and provided a hierarchical representation through the dendrogram.

DBSCAN provided a density-based perspective and identified four clusters along with ten noise observations using the selected parameters.

The resulting customer segments provide useful business information for targeted marketing, loyalty programs, personalized offers, discounts, and customer engagement strategies.

K-Means provides the primary interpretable segmentation for this project, while Hierarchical Clustering and DBSCAN provide complementary perspectives on the customer structure.

---

# Project Visualizations

The project contains the following visualizations:

1. Age Distribution with KDE
2. Annual Income Distribution with KDE
3. Spending Score Distribution with KDE
4. Pairplot
5. Correlation Heatmap
6. K-Means Elbow Method
7. K-Means Silhouette Score
8. K-Means Cluster Visualization
9. Hierarchical Dendrogram
10. Hierarchical Cluster Visualization
11. 4-NN Distance Plot
12. DBSCAN Cluster Visualization
13. K-Means vs Hierarchical Comparison
14. Three-Algorithm Comparison

---

# Repository Structure

```text
Mail_Customer_Segmentation/
│
├── Mail_Customer_Segmentation.ipynb
├── Mall_Customers.csv
├── Unsupervised_Learning_PR1_Final_Conclusion.pdf
├── README.md

```

---

# Technologies Used

| Technology | Purpose |
|---|---|
| Python | Programming Language |
| Pandas | Data Manipulation |
| NumPy | Numerical Computing |
| Matplotlib | Data Visualization |
| Seaborn | Statistical Visualization |
| Scikit-learn | Machine Learning |
| SciPy | Hierarchical Clustering |
| Jupyter Notebook | Notebook Environment |
| Google Colab | Notebook Execution |

---

# Installation

## Clone the Repository

```bash
git clone https://github.com/patelneel9080/Mail_Customer_Segmentation.git
```

## Navigate to the Project

```bash
cd Mail_Customer_Segmentation
```

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

# Requirements

Create a file named:

```text
requirements.txt
```

Add:

```text
pandas
numpy
matplotlib
seaborn
scikit-learn==1.4.0
scipy
```

---

# How to Run

## Using Google Colab

1. Open `Mail_Customer_Segmentation.ipynb`.
2. Open the notebook in Google Colab.
3. Upload `Mall_Customers.csv`.
4. Run the cells from beginning to end.
5. Review the generated tables and visualizations.

## Using Jupyter Notebook

Run:

```bash
jupyter notebook Mail_Customer_Segmentation.ipynb
```

Then execute all notebook cells sequentially.

---

# Screenshots

Important project plots should be stored inside the `screenshots` directory.

The required screenshots include:

- Elbow Method
- Silhouette Score
- K-Means Clusters
- Dendrogram
- 4-NN Distance Plot
- DBSCAN Clusters
- Three-Panel Algorithm Comparison

---

# Project Video

The project explanation video should demonstrate:

- Why feature scaling is required
- Elbow Method
- Silhouette Score
- Dendrogram
- DBSCAN parameters
- Algorithm comparison
- Customer segments
- Business insights

## Video Link

Add the video URL here after uploading it:

```text
PASTE_VIDEO_LINK_HERE
```

---

# Git Commit History

Recommended meaningful commits:

```text
Add EDA section with pairplot and correlation heatmap
```

```text
Build K-Means clustering with Elbow and Silhouette analysis
```

```text
Add Hierarchical Clustering and dendrogram analysis
```

```text
Add DBSCAN tuning and clustering comparison
```

```text
Add project documentation and requirements
```

---

# Project Status

| Component | Status |
|---|---|
| Dataset Loading | Completed |
| Dataset Inspection | Completed |
| Data Preprocessing | Completed |
| Gender Encoding | Completed |
| Feature Scaling | Completed |
| Exploratory Data Analysis | Completed |
| K-Means Clustering | Completed |
| Hierarchical Clustering | Completed |
| DBSCAN Clustering | Completed |
| Model Evaluation | Completed |
| Algorithm Comparison | Completed |
| Customer Segmentation | Completed |
| Business Insights | Completed |
| Final Conclusion | Completed |
| Documentation | Completed |

---

# Author

**Neel Patel**

GitHub:

https://github.com/patelneel9080

---

# License

This project is created for academic and educational purposes.

The Mall Customer Segmentation dataset is sourced from Kaggle and is used according to its applicable dataset license.

---
