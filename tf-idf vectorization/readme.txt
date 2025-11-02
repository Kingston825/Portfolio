Movie Review Sentiment Classification Project
This is a text-based version of the project documentation, outlining the steps taken for sentiment classification using movie reviews.

1. Data Preparation and Stemming
The project starts by loading the data and performing text preprocessing, including stemming, which was also done in Week 3.
Load Data: Data is read from 'labeled TrainData.tsv'.

x: the review text.
y: the sentiment (target variable).



Preprocessing Function (clean_text) :

Removes punctuation.
Splits text into tokens.
Applies Porter Stemmer.
Removes English stop words.


2. Train-Test Split and TF-IDF Vectorization
The data is split and vectorized for model training.

Split Data: The data is split into training and test sets.


TF-IDF Vectorization:
The TfidfVectorizer is fitted and transformed on the training set (x_train).

It is then only transformed (not fitted) on the test set (x_test).

Rationale for NOT Fitting TF-IDF to the Test Set
The vectorizer is 

NOT fitted to the test set to prevent data leakage. Fitting on the test set would allow the model to learn the vocabulary and inverse document frequencies (IDF) from the test data, which would not be available in a real-world scenario. This leads to an unrealistically optimistic performance evaluation.


3. Model 1: Logistic Regression
A Logistic Regression model is trained and evaluated.


Model Training: LogisticRegression().fit(x_train, y_train).



Predictions: y_pred is generated on the test set.

Evaluation on Test Set:


Accuracy: 0.8828.
Precision: 0.8747.
Recall: 0.8943.
F1-Score: 0.8844.



4. Model 2: Random Forest Classifier
The steps are repeated for a different classification model, the Random Forest Classifier.


TF-IDF (for RF): The data is re-vectorized, this time with max_features=500.


tfidf.fit_transform(x_train).
tfidf.transform(x_test).
Model Training: RandomForestClassifier with n_estimators=100 and random_state=42 .
Predictions: y_pred is generated on the test set.

Evaluation on Test Set:


Accuracy: 0.8396.
Precision: 0.8477.
Recall: 0.8237.
F1-Score: 0.8355.


Confusion Matrix: Created using confusion_matrix(y_test, y_pred).


ROC Curve: Generated using roc_curve with predicted probabilities (y_pred_proba) .