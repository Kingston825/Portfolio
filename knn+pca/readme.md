# README: ALS Patient Data Clustering Analysis

---

## 🧐 Project Overview

This project performs an unsupervised machine learning analysis on a dataset related to ALS (Amyotrophic Lateral Sclerosis) patients. The primary goal is to identify distinct patient clusters using K-means clustering and then visualize these clusters in a two-dimensional space using Principal Component Analysis (PCA).

---

## 📁 Data Source

* **File:** `als_data.csv`
* **Initial Shape:** 2223 rows × 101 columns

---

## 🛠️ Project Workflow

The analysis follows these key steps:

### 1. Data Preprocessing

* **Remove Irrelevant Data:** The `ID` and `SubjectID` columns were dropped as they are not relevant for clustering.
* **Handle Missing Data:** Any rows containing null values were dropped to ensure data integrity for the models.
* **Data Scaling:** The entire dataset was scaled using `StandardScaler` to normalize the feature ranges, which is essential for both K-means and PCA.

### 2. K-means Clustering & Model Selection

* **Objective:** To find the optimal number of clusters (K) that best segment the patient data.
* **Method:** The **Silhouette Score** was calculated for a range of cluster numbers.
* **Analysis:** A plot of the Silhouette Score vs. the Number of Clusters was generated to identify the "elbow" or the point representing the most distinct and well-separated clusters.
* **Model Fitting:** A final K-means model was fit to the scaled data using the optimal number of clusters determined from the silhouette analysis.

### 3. Dimensionality Reduction & Visualization

* **Technique:** **Principal Component Analysis (PCA)** was applied to the scaled dataset to reduce its 99 dimensions down to 2 principal components.
* **Visualization:** A scatterplot of the 2-component PCA data was created, with each point colored according to its assigned cluster from the K-means model. This plot helps visualize the separation and grouping of the patient data in a 2D space.

### 4. Summary & Conclusion

The project concludes with a summary of the results, interpreting the final cluster visualization and the insights gained from segmenting the ALS patient data.

---

## 📦 Dependencies

* `pandas`
* `numpy`
* `matplotlib.pyplot`
* `seaborn`
* `sklearn.preprocessing.StandardScaler`
* `sklearn.cluster.KMeans`
* `sklearn.metrics.silhouette_score`
* `sklearn.decomposition.PCA`