# Diabetes Risk Classification

This project was done for The University of Washington's Professional Master's Program AI and Healthcare course taught by Dr. Karthik Mohan.

## Introduction

A binary classification problem with target classes 1 referring to high risk and 0 referring to low risk of chronic diabetes. The focus was on explainable models, and as such a Decision Tree (DT) was used to generate explainable pathways to each prediction. I achieved a maximum of 0.86 as the f1 score using a Logistic Regression (LR) model and 0.76 with the use of the DT.

## Dataset

The data contained 10 numeric features: age, sex, body mass index, average blood pressure and six blood serum measurements (s1-s6 in the dataframe below). As previously stated the target is binary classification, high risk or low risk of chronic diabetes.

<img width="445" alt="Screen Shot 2022-07-12 at 4 15 42 PM" src="https://user-images.githubusercontent.com/72525765/178614086-d7252f11-005e-4435-a181-89c88e11eda2.png">

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

## Results

## The code

