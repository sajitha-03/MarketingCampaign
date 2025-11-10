# MarketingCampaign

Jupyter Notebook : https://github.com/sajitha-03/MarketingCampaign

## Overview
The goal of the project is to compare the performance of the classifiers namely KNearestNeighbor, LogisticRegression, DecisionTrees, and SupportVectorMachines utilizing a dataset related to marketing bank products over the telephone.

## Problem Statement
Given a dataset of directed marketing campaigns collected from a Portugese bank, the objective is to predict if a client will subscribe to a term deposit. This predictve model would help the bank target clients effectively, reducing campaining expense and improving marketing efficiency.

## Data Understanding
The dataset comes from the UCI Machine Learning repository [link](https://archive.ics.uci.edu/ml/datasets/bank+marketing). The data is from a Portugese banking institution and is a collection of the results of multiple marketing campaigns - an aggregate of 17 marketing campaigns. On examining the dataset, the data can be grouped to 3 categories - client profile, campaign attributes and previous data, and economic attributes.

Key observations:
- No missing data and duplicate entries
- Lot of unknown values
- Dataset is imbalanced with only 13% subscribed to the deposit

## Data Preparation
- Dropped 'unknown' entries
- Dropped 'duration' feature as it is a post-event variable
- Applied StandardScaler to scale on numerical features
- Applied OneHotEncoding on catergorical features
- Split train and test data for simple cross validation
- Dataset after data preprocessing - (30488, 20)

## Modeling
All features - client, campaign and economic attributes used for modeling. Compared the performance of different models such as KNearestNeighbor, LogisticRegression, DecisionTrees, and SupportVectorMachines.

## Findings
### Comparing accuracy score and fit time between classifiers

#### Baseline accuracy: 

- Baseline Train Accuracy: 87.43%
- Baseline Test Accuracy: 86.98%

#### Default settings:

<img width="419" height="149" alt="Screenshot 2025-11-07 at 7 30 31 PM" src="https://github.com/user-attachments/assets/0d5d8dc4-d866-4a0d-a2f0-f061b09a5fe8" />


- All models outperform the baseline (~87%) on the test set.
- Logistic Regression and SVM both yield the best test accuracy (88.5-88.6%).
- The Decision Tree clearly overfits, achieving 99% on training but drops to 82% on test data.
- KNN performs decently but is computationally heavier for larger datasets.

#### Improving the model with hyperparameters and GridSearchCV:
**Best params:**


<img width="663" height="121" alt="Screenshot 2025-11-07 at 7 30 54 PM" src="https://github.com/user-attachments/assets/16bb9491-134a-46b4-b18d-92e2f4cfea9a" />


<img width="466" height="131" alt="Screenshot 2025-11-07 at 7 31 09 PM" src="https://github.com/user-attachments/assets/a93b62dd-9365-438b-bf58-a46bba08e48d" />


- Hyperparameter tuning improved Decision Tree performance significantly — the test accuracy rose from 82% → 88.7% with reduced overfitting and better generalization (depth limited to 5).
- SVM remains competitive in accuracy but has very high training time (~65 s).
- Logistic Regression remained stable and consistent
- KNN showed minimal improvement and moderate runtime increase

Choosing the tuned Decision Tree (max_depth=5, criterion='entropy') to investigate feature importance — it balances strong performance with transparent, actionable insights on what drives customer subscriptions.

#### Feature Importance

<img width="862" height="551" alt="Screenshot 2025-11-07 at 7 31 31 PM" src="https://github.com/user-attachments/assets/dda343f3-d215-4141-a8ae-6a57ef03f194" />

- Macroeconomic factors such as labor market conditions (nr_employed), how confident consumers feel about the economy (cons.conf.indx) and interest rate(euribor3m) are few of the top 10 features that influence the subscription probabilty
- Targeting clients who have shown previous outcome as succesful would also increase the effectiveness of the campaign

## Next Steps and Recommendations

Since the data is imbalanced (≈88% “no”), focus on metrics that better reflect minority-class performance:

- Precision, Recall, F1-score for class y = "yes".
- ROC-AUC score and confusion matrix to assess trade-offs.

A marketing campaign while the economic conditions are healthy and stable, would give better insights on the impact on client profile and campaign specific attributes.

