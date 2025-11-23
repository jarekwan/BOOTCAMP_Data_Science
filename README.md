# Supplier Segmentation using Clustering

## Project Overview
This project focuses on segmenting suppliers based on numerical performance metrics. The goal is to identify natural groups related to cost, quality, delivery performance, and operational stability. Such segmentation supports data-driven procurement decisions, helps identify high-risk suppliers, and enables better resource allocation. This notebook was developed as a Data Science Bootcamp final assignment.

## Dataset Description
The dataset consists of numerical features describing supplier behavior and performance. Each record represents one supplier. Typical characteristics may include delivery delay, defect rate, cost efficiency, response time, reliability indicators, and process stability. Only numerical columns were preserved for modeling to ensure compatibility with PCA and clustering.


##Colab links:
PROJECT_DATASCIENCE:https://colab.research.google.com/drive/1Gixb_xdjTX2q7ozwc3yIExg-ibh0yLJ-?usp=sharing

PROJECT_DATASCIENCE2:https://colab.research.google.com/drive/1ve87017qSmzaeKZ1eWp922y62cYRbjoX?usp=sharing

## Methodology

### Exploratory Data Analysis (EDA)
Initial exploration included:
- summary statistics,
- missing value inspection,
- value distributions,
- outlier detection,
- correlation analysis.

### Data Preparation
Several preprocessing steps were applied:
- creation of a working copy of the dataset,
- removal of non-numerical columns,
- median imputation of missing values,
- feature scaling using StandardScaler (required for PCA and K-Means),
- optional removal of highly correlated features (correlation > 0.9).

### Dimensionality Reduction (PCA)
Principal Component Analysis was applied to reduce dimensionality while retaining most variance. Components were selected based on cumulative explained variance, targeting at least 90 percent coverage. The first two components were used for visualization.

### Clustering Algorithms
Two clustering methods were applied:

K-Means:
- evaluation of multiple cluster counts using Elbow and Silhouette methods,
- final selection based on maximum silhouette score,
- visualization in PCA space.

DBSCAN:
- grid search over multiple eps and min_samples values,
- selection based on the highest silhouette score,
- ability to detect noise and outlier suppliers.

### Evaluation and Comparison
Model quality was evaluated using silhouette score. Cluster profiles were created based on average z-scores of features. Heatmaps were used for human-readable interpretation. An automatic labeling method selected the most dominant features describing each cluster.

## Results Summary
The clustering process successfully separated suppliers into distinct performance groups. K-Means produced stable, interpretable clusters of suppliers. DBSCAN detected sparse outliers and noise, useful for risk monitoring. PCA significantly improved separation and interpretability.

## How to Run
1. Clone the repository:
