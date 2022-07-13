# Diabetes Risk Classification

This project was done for The University of Washington's Professional Master's Program AI and Healthcare course taught by Dr. Karthik Mohan.

## Introduction

A binary classification problem with target classes 1 referring to high risk and 0 referring to low risk of chronic diabetes. The focus was on explainable models, and as such a Decision Tree (DT) was used to generate explainable pathways to each prediction. I achieved a maximum of 0.86 as the f1 score using a Logistic Regression (LR) model and 0.76 with the use of the DT.

## Dataset

The data contained 10 numeric features: age, sex, body mass index (bmi), average blood pressure and six blood serum measurements (s1-s6 in the dataframe below). As previously stated the target is binary classification, high risk or low risk of chronic diabetes. This data was normalized using Scikit-learn's normalize method, the StandardScaler was also tried but found to be less effective in the end result. 

<img width="445" alt="Screen Shot 2022-07-12 at 4 15 42 PM" src="https://user-images.githubusercontent.com/72525765/178614086-d7252f11-005e-4435-a181-89c88e11eda2.png">

## Correlation

In an effort to determine which feature had the heaviest weight on the target, I built a correlation matrix and colored it like a heatmap. From analyzing the resulting heatmap we can see that features like s3, and sex are heavily and weakly respectively, negatively correlated with the target. Whereas the features like bmi and s5 are actually postively correlated.

<img width="284" alt="Screen Shot 2022-07-12 at 4 26 35 PM" src="https://user-images.githubusercontent.com/72525765/178615146-8b5f9c22-31d9-43e6-bc49-259478a2a837.png">

## Models

Logistic Regression
- *max_iter:* 300
- *penalty:* elasticnet
- *l1_ratio:* 0.4
- *solver:* saga
- *C:* 67

Decision Tree
- *criterion:* entropy
- *max_depth:* 5

## Feature Importance

In analysis of the feature importance of both the LR and DT models, the top feature was blood serum measurement s4. Looking at s4 in the correlation heatmap above, we can claim that the the feature s4 has mild to strong positive correlations with a lot of the other features, as well as a strong negative correlation with the feature s3, and a mild positive correlation with the target. Since both models agree on the top feature we can claim that this feature s4 gives the most information for both the LR and DT models. 

Here we have the feature importance extracted from the LR model (left) and from the DT model (right) graphed against their feature names

<img width="279" alt="Screen Shot 2022-07-12 at 4 40 51 PM" src="https://user-images.githubusercontent.com/72525765/178616391-aa6fa6d2-20dd-4246-9e10-7c4a147c25bc.png"> <img width="284" alt="Screen Shot 2022-07-12 at 4 41 12 PM" src="https://user-images.githubusercontent.com/72525765/178616418-8f788fa7-21e0-4932-bbbd-313128ee7c4f.png">

## DT Explainability

In order to have a model be explainable, I needed something visually interpretable. For this I simply used the DT model as I already had the model trained to an acceptable accuracy. To explain to the reader why the DT arrived at the prediction it did, this is assisted by a DT graphed out in the notebook which is helpful for graphical explanation, I generated a function which uses the DT models decision_path function which accepts a feature list as a sample and returns a path. This path was then followed, with each feature name and threshold value being printed with the feature value at that split so the user can confirm which direction it went was the correct one. Below are 3 examples of positive predictions and 1 negative prediction.

<img width="855" alt="Screen Shot 2022-07-12 at 5 06 31 PM" src="https://user-images.githubusercontent.com/72525765/178619272-c1a205d3-854b-41a0-b74d-af7c8b8ccdc7.png">

## Results

In the table below I generated metrics for the validation data for the LR and DT model, as shown the LR model outperformed the DT by ~0.1. The LR model was a good general model as well for this data as the f1 score for the unseen Kaggle data was similar, actually better, than the validation data.

<img width="927" alt="Screen Shot 2022-07-12 at 4 50 45 PM" src="https://user-images.githubusercontent.com/72525765/178617230-e907a820-ffc0-4c66-be9c-ed2572449917.png">

## The code
You can find the code with all the intermediate steps and results in the notebook on this repo directory. Feel free to download and use the methods crated here for DT explainability or feature importance graphing! Enjoy!
