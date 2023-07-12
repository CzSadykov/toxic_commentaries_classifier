# Classification of texts for an online store

**Prerequisites:** Wikishop is launching a new service. Now users can edit and supplement product descriptions, just like in wiki communities. I.e. clients propose their edits and comment on the changes of others.

**Goal:** creating a tool that will look for toxic comments and submit them for moderation.

**Task:** building a model for classifying comments into positive and negative.

**Data:** Tweets with edit toxicity markup. ```Tag:``` comment text. ```Target trait:``` binary toxicity classification.

**Requirements:**

* The F1 metric must be at least 0.75.

## Results

**1. Preprocessing.**

So that's what we've done: 

* Downloaded and studied the data, revealed an imbalance in the classes of the target trait;
* Prepared data for training: cleaned, lemmatized and divided into samples;
* Created a pipeline for data vectorization during model cross-validation in order to prevent data leakage.

**2. Training.**

* With the help of randomized selection, we selected the best hyperparameters for models without gradient boosting and with it: logistic regression, Light GBM and CatBoost;
* Discovered that **F1-measure of models is higher if the imbalance of classes is not eliminated**;
* Compared model metrics (training time and F1 value) taking into account training time, hyperparameter fitting and cross-validation. Based on the results of the comparison, we chose simple **logistic regression** with the highest F1(**0.771**);
* Hyperparameters of the selected model: {'max_iter': 100, 'C': 16}.

**3. Testing.**

* We evaluated the quality of predictions of the selected model on the test sample.
* Calculated a final F1 score of **0.775**, which is higher than the given threshold of 0.75.
* Checked the model for adequacy using a constant model whose F1 score was 0.184.
