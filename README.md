# LTFS-Hackathon-2021
This was an Online Hackathon conducted by Analytics Vidhya on their website from Jan 30 - Feb 7 2021.
https://datahack.analyticsvidhya.com/contest/ltfs-data-science-finhack-3/

## Introduction:-
**LTFS Top-Up loan Up-Sell Prediction**
* Loans are usually provided to Industries, Corporates and Individuals. The interest from those loans are the main source of income for the provider.
* A **top-up loan** is a facility of availing further funds on an existing loan.
* LTFS provides is interested in selling more of its Top-up loan services to its existing customers so they have decided to identify when to pitch a Top-up during the original loan tenure.
* If they correctly identify the most suitable time to offer a top-up, this will ultimately lead to more disbursals and can also help them beat competing offerings from other institutions.

## Problem Statement:-
It was a multi-class classification problem with high class imbalance. Participants were scored based on macro averaged F1 score.

## Model Selection:-
The model creation part was split into 2 broad categories:-
1. Determine if the person will take a Top-Up loan or not. (Binary Classification)
2. If the person is likely to take a Top-Up loan, then determine when they are going to. (Multi-Class classification)

Modelling techniques used:-
1. Created a 5 fold CV with 80:20 train-test split.
2. Created and tuned hyper-parameters for 7 different models:-
    * Logistic Regression (Recursive 1 vs all method)
    * Multinomial Naive Bayes (Recursive 1 vs all method)
    * K Nearest Neighbours
    * Support Vector Classifier (Recursive 1 vs all method)
    * Random Forest
    * XGBoost
    * Deep Neural Network
3. Random Forest was selected as the final model.

## Feature Engineering & Selection:-
1. Features having nulls > 20% were dropped if those features were highly speculative.
2. Feature cleaning was performed on columns where the data format was wrong or useful data was found appended with jargons. Other data included lists or comma separated values as a single entry where sum/mean were taken to aggregate those data.
3. Since there were multiple entries for same IDs in the bureau data, those rows were aggregated using a host of techniques based on column type and data significance.
4. Low cardinality categorical variables were encoded with One-Hot encoding.
5. High cardinality categorical variables were encoded with CatBoost response based encoding.
6. Some synthetic features were also created to portray other derived values from few base features.
7. SelectKbest automated feature selection criteria was used with mutual information as scoring function.

## Model Hyper Parameter Tuning:-
A bayesian tuning method through Hyperopt library was employed on each model with their respective hyper-parameter space. F1-macro on a 5-fol CV was used as the measure for model performance.
