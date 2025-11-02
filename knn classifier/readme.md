README.md

---



\## README: Loan Status Classification and Model Tuning



---



\## 🧐 Project Overview



This project focuses on building, tuning, and comparing different classification models to predict the \*\*Loan Status\*\* (`Loan\_Status`) based on applicant data. The methodology involves data preparation, establishing a modeling pipeline, and using \*\*Grid Search with cross-validation\*\* to identify the optimal model and hyperparameters across \*\*K-Nearest Neighbors (KNN)\*\*, \*\*Logistic Regression\*\*, and \*\*Random Forest\*\* classifiers.



---



\## 📁 Data



\### Source and Preparation



\* \*\*Dataset:\*\* `Loan\_Train.csv`

\* \*\*Target Variable:\*\* `Loan\_Status`

\* \*\*Data Cleaning:\*\*

&nbsp;   \* The redundant `Loan\_ID` column was dropped.

&nbsp;   \* All rows with missing data were removed, resulting in a processed dataset of \*\*(480, 12)\*\* rows/columns, down from an initial \*\*(614, 13)\*\*.

&nbsp;   \* All categorical features were converted into \*\*dummy variables\*\* (one-hot encoding).

\* \*\*Data Split:\*\* The final processed data (21 columns) was split into training and testing sets with a test size of \*\*20%\*\*.



---



\## 🛠️ Methodology and Model Tuning



\### Modeling Pipeline



A sequential \*\*Pipeline\*\* was established for robust modeling and parameter tuning. This pipeline ensures that data scaling is performed correctly within the cross-validation loops, preventing data leakage.



1\.  \*\*StandardScaler\*\*

2\.  \*\*MinMaxScaler\*\*

3\.  \*\*Classifier\*\* (varied for each test)



\### Phase 1: K-Nearest Neighbors (KNN) Tuning



The initial evaluation used the default \*\*KNN Classifier\*\* within the pipeline:

\* \*\*Default KNN (n\\\_neighbors=5) Test Accuracy:\*\* \*\*0.6875\*\* (68.75%)



A \*\*Grid Search\*\* with \*\*5-fold cross-validation\*\* was then used to tune the `n\_neighbors` parameter:

\* \*\*KNN Search Space:\*\* `n\_neighbors` varied from \*\*1 to 10\*\*.

\* \*\*Best KNN Hyperparameter:\*\* `n\_neighbors` = \*\*7\*\*.

\* \*\*Tuned KNN Test Accuracy:\*\* \*\*0.71875\*\* (71.88%).



\### Phase 2: Comprehensive Model Search



The search space was expanded to include Logistic Regression and Random Forest to find the absolute best model for the dataset.



\* \*\*Expanded Search Space:\*\*

&nbsp;   \* \*\*Logistic Regression:\*\* `LogisticRegression(max\_iter=500)`

&nbsp;   \* \*\*Random Forest:\*\* `RandomForestClassifier()`

\* \*\*Best Model Found:\*\* The grid search identified \*\*LogisticRegression\*\* as the best estimator.

\* \*\*Best Hyperparameters:\*\* `LogisticRegression(max\_iter=500)`

\* \*\*Best Model Test Accuracy:\*\* \*\*0.7395833333333334\*\* (73.96%).



---



\## 📊 Summary of Results



The hyperparameter tuning and model comparison successfully improved the classification accuracy.



| Model | Hyperparameters | Test Accuracy |

| :--- | :--- | :--- |

| \*\*Initial KNN\*\* | Default (n\\\_neighbors=5) | 68.75% |

| \*\*Tuned KNN\*\* | n\\\_neighbors=7 | 71.88% |

| \*\*Best Overall Model\*\* | \*\*LogisticRegression(max\\\_iter=500)\*\* | \*\*73.96%\*\* |



The exercise demonstrates the importance of model selection and hyperparameter tuning, as the accuracy score significantly improved from the initial 68.75% to the final 73.96%.

