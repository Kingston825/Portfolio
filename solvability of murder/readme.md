# README: Healthcare Data Classification

---

## 🧐 Project Overview

This project involves a comprehensive Exploratory Data Analysis (EDA) and the development of a predictive classification model using a healthcare dataset. The primary goal is to preprocess the data, build a `DecisionTreeClassifier`, and evaluate its performance in predicting the target variable.

---

## 📁 Data

* **Source:** `healthcare_dataset.csv`
* **Target Variable:** `target`

---

## 🛠️ Project Workflow

### 1. Exploratory Data Analysis (EDA)

* The dataset was loaded and inspected.
* Histograms were generated for all numerical features to visualize their distributions.

### 2. Data Preprocessing

To prepare the data for modeling, the following steps were taken:

* **Dropping Columns:** The `Patient_ID` column was removed as it is not a predictive feature.
* **One-Hot Encoding:** Categorical features were converted into numerical format using `pandas.get_dummies`.
* **Train-Test Split:** The data was split into training and testing sets.
* **Feature Scaling:** `StandardScaler` was applied to both the training and test sets to normalize the data.

### 3. Model Training & Evaluation

* **Model:** A `DecisionTreeClassifier` was chosen for this task, configured with the `criterion='entropy'`.
* **Training:** The model was fit to the scaled training data.
* **Predictions:** The trained model was used to make predictions on the scaled test set.

---

## 📊 Results

The model's performance was assessed using a confusion matrix and a classification report.

* **Accuracy:** The final model achieved an accuracy of approximately **66%**.
* **Classification Report:**
    * The precision for both classes ("No" and "Yes") was 66%.
    * The recall was 65% for "No" and 67% for "Yes".
    * The report noted that after resolving an initial oversampling problem, the false positives and false negatives were similarly balanced.

---

## 📦 Dependencies

* `pandas`
* `matplotlib.pyplot`
* `numpy`
* `sklearn.model_selection.train_test_split`
* `sklearn.preprocessing.StandardScaler`
* `sklearn.tree.DecisionTreeClassifier`
* `sklearn.metrics.confusion_matrix`
* `sklearn.metrics.classification_report`