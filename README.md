# Predicting Credit Risk with Supervised Machine Learning

## Overview

Machine learning models have proven invaluable in the loan and credit industry, accelerating the rate at which credit applications can be assessed. A process that once took ages to complete, various algorithms now can be used to predict whether a loan application will be low- or high-risk with a high degree of accuracy. Herein, supervised machine learning models like Logistic Regression or Decision Trees aim to predict a credit application's positive or negative status by assessing input data like loan amount, credit history, and demographic information. In this analysis, six machine learning models were tested against a large dataset of credit card applications to predict credit risk.

### Dataset

The dataset of 68,817 rows and 86 columns of loan application data was then separated into the loan application's *input features* like loan amount, credit history, and demographic information from the *target variable,* which classifies the loan application's status as either low- or high-risk. This dataset was then used to train various supervised machine learning models to predict credit risk based on a loan application's input features. Preliminary analysis of the dataset shows a total of 68,817 rows spread over 86 columns of variable datatypes. After separating the *input features* from the *target variable,* it was noted that a considerable imbalance exists between the value counts of each binary outcome in the *target variable* (low-risk 1: 68,470 | high-risk 1: 347).

### Logistic Regression & Sampling Methods

Logistic Regression models predict a binary classification based on input variables. These model types use a sigmoid curve to calculate the probability that a data point will fall within one category or another. While a Logistic Regression model would theoretically do a good job of classifying a balanced loan application dataset as either low- or high-risk, unbalanced datasets cause undue bias in the machine learning model toward the majority class. To overcome this limitation, various Over- and Under-Sampling techniques can be applied to better train the Logistic Regression model. Over-Sampling, like its namesake, involves oversampling the minority class until both classes are even before training the Logistic Regression model. Under-Sampling, on the other hand, involves minimizing the sample size of the majority class before further analysis. A third option, Combination Over- and Under-Sampling, produces a balanced sample dataset that evades the potential noise of Over-Sampling and data loss of Under-Sampling methods. Due to the credit application dataset's large size and *target variable* imbalance, a variety of Over-/Under-Sampling methods will be necessary before Logistic Regression models can predict the credit application's binary outcome as low- or high-risk[^1].

### Decision Trees & Ensemble Classifiers

Like the other supervised machine learning model described above, Decision Trees are trained using input data to predict a data point's binary classification or target variable. Decision Tree models are relatively impervious to the linear features of a dataset and make a good candidate for testing with credit application data. These models work by deriving a series of conditions from the input features, which are then used to determine a test point's binary outcome[^2]. This analysis tests Ensemble Classifiers, an advanced decision tree model type that combines multiple trees into one, improving performance over a single tree model[^3].

## Results

The machine learning algorithms tested before Logistic Regression include two Over-Sampling Models (RandomOverSampler, SMOTE), an Under-Sampling model (ClusterCentroids), a Combination Over-/Under-Sampling model (SMOTEENN). Two Ensemble Classifiers (BalancedRandomForestClassifier, EasyEnsembleClassifier) were also tested against this dataset. All models were evaluated based on the following metrics:

+ Balanced Accuracy Score - comparing the accuracy of the predicted target values compared to the actual target values
+ Confusion Matrix - displaying the number of predicted/actual outcomes
    + Binary Value 0: 
    + Binary Value 1:
+ Imbalanced Classification Report - presenting the precision, recall, specificity, f1 score, geometric mean, and index balanced accuracy

The results for the Sampling + Logistic Regression models are as follows:

- Over-Sampling
    - Random Over-Sampling
        - Balanced Accuracy Score: 0.7855483842376043
        - Confusion Matrix:
            |        |Predicted 0[^*]|Predicted 1[^**]|
            |--------|-----------|-----------|
            |Actual 0|         62|         25|
            |Actual 1|       2423|      14695|
        - Classification Report:
            |         | Precision| Sensitivity| Specificity|  f1 Score|   *n*|
            |---------|----------|-------|------------|----------|-----|
            |        0|0.02|0.71|0.86|0.05|   87|
            |        1|1.00|0.86|0.71|0.92|17118|
            |avg/total|0.99|0.86|0.71|0.92|17205|
    - SMOTE (Synthetic Minority Oversampling Technique)
        - Balanced Accuracy Score: 0.7958883772274395
        - Confusion Matrix:
            |        |Predicted 0|Predicted 1|
            |--------|-----------|-----------|
            |Actual 0|         62|         25|
            |Actual 1|       2069|      15049|
        - Classification Report:
            |  |Precision| Sensitivity|Specificity|f1 Score|*n*|
            |--|---------|------------|-----------|--------|---|
            |        0|0.03|0.71|0.88|0.06|   87|
            |        1|1.00|0.88|0.71|0.93|17118|
            |avg/total|0.99|0.88|0.71|0.93|17205|
- Under-Sampling
    - Cluster Centroids
        - Balanced Accuracy Score: 0.5442661782548694
        - Confusion Matrix:
            |        |Predicted 0|Predicted 1|
            |--------|-----------|-----------|
            |Actual 0|         70|         31|
            |Actual 1|      10340|       6764|
        - Classification Report:
            |         | Precision| Sensitivity| Specificity|  f1 Score|   *n*|
            |---------|----------|-------|------------|----------|-----|
            |        0|0.02|0.78|0.77|0.03|   87|
            |        1|1.00|0.77|0.78|0.87|17118|
            |avg/total|0.99|0.77|0.78|0.86|17205|
- Combination Over-/Under-Sampling
    - SMOTEENN (Synthetic Minority Oversampling Technique + Edited Nearest Neighbor)
        - Balanced Accuracy Score: 0.7750200434307908
        - Confusion Matrix:
            |        |Predicted 0|Predicted 1|
            |--------|-----------|-----------|
            |Actual 0|         68|         19|
            |Actual 1|       3964|      13154|
        - Classification Report:
            |         | Precision| Sensitivity| Specificity|  f1 Score|   *n*|
            |---------|----------|-------|------------|----------|-----|
            |        0|0.03|0.72|0.87|0.05|   87|
            |        1|1.00|0.87|0.72|0.93|17118|
            |avg/total|0.99|0.87|0.72|0.93|17205|

The results for the Ensemble Classifier models are as follows:

- Ensemble Classifiers
    - Balanced Random Forest Classifier
        - Balanced Accuracy Score: 0.7872122911555088
        - Confusion Matrix:
            |        |Predicted 0|Predicted 1|
            |--------|-----------|-----------|
            |Actual 0|         58|         29|
            |Actual 1|       1579|      15539|
        - Classification Report:
            |         | Precision| Sensitivity| Specificity|  f1 Score|   *n*|
            |---------|----------|-------|------------|----------|-----|
            |        0|0.04|0.67|0.91|0.07|   87|
            |        1|1.00|0.91|0.67|0.95|17118|
            |avg/total|0.99|0.91|0.67|0.95|17205|
    - Easy Ensemble AdaBoost Classifier
        - Balanced Accuracy Score: 0.9171974650599691
        - Confusion Matrix:
            |        |Predicted 0|Predicted 1|
            |--------|-----------|-----------|
            |Actual 0|         78|          9|
            |Actual 1|       1064|      16054|
        - Classification Report:
            |         | Precision| Sensitivity| Specificity|  f1 Score|   *n*|
            |---------|----------|-------|------------|----------|-----|
            |        0|0.07|0.90|0.94|0.13|   87|
            |        1|1.00|0.94|0.90|0.97|17118|
            |avg/total|0.99|0.94|0.90|0.96|17205|



## Summary

The machine learning model with the best Accuracy, Precision, and F1 Scores was the Easy Ensemble Classifier (91.7%, prec=0.99, f1=0.96). This was followed by the SMOTE oversampling Algorithm (79.6%, prec=0.99, f1=0.93) and the Balanced Random Forest Classifier (78.7%, prec=0.99, f1=0.95)). The Cluster Centroids Undersampling Algorithm had the lowest accuracy, precision, and f1 scores, receiving 54.4%, 0.99, 0.86, respectively. 

The Easy Ensemble AdaBoost Classifier provided the best balanced accuracy and f1 score out of the six machine learning models tested. I would recommend using an ensemble classifier since these machine learning models are generally resistant to linear features of the data, and provide the best accuracy in predicting credit risk. 

## References
[^1]: edX Boot Camps LLC. (2023). How Logistic Regression Works. Bootcamp: UCB-VIRT-DATA-PT-08-2022-U-B-MW Page 18.3.3. Retrieved January 24, 2023, from https://courses.bootcampspot.com/courses/2315/pages/18-dot-3-3-how-logistic-regression-works?module_item_id=743247 
[^2]: Roy, A. (2020, November 6). A dive into decision trees. Medium. Retrieved January 24, 2023, from https://towardsdatascience.com/a-dive-into-decision-trees-a128923c9298 
[^3]: Nagpal, A. (2017, October 18). Decision tree ensembles- bagging and boosting. Medium. Retrieved January 24, 2023, from https://towardsdatascience.com/decision-tree-ensembles-bagging-and-boosting-266a8ba60fd9#:~:text=Ensemble%20methods%2C%20which%20combines%20several,to%20form%20a%20strong%20learner
[^*]: low-risk
[^**]: high-risk
