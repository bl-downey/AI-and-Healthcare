# Stress Classification

This project was done for The University of Washington's Professional Master's Program AI and Healthcare course taught by Dr. Karthik Mohan.

## Introduction

This project I performed data cleaning, different imputation methods, constructed a few different models for comparison and analyzed feature importance for the dataset from this paper: https://dspace.mit.edu/handle/1721.1/9067

## Dataset

The dataset had 3159 samples which were cleaned and imputeted as a whole before being broken into train and validation. The original feature count for this was 13 not including Id or Target. 

The data can be downloaded from this repo -- it is the original dataframe before cleaning and imputation. 

## Data Cleaning

To begin the cleaning process I iterate through the features and determine which features are unimportant / have a considerable number of 0's or NaN values. The features LF, HF and LF_HF were removed.

## Imputation

I tried various different imputation methods including: Mean, Median, Hot Deck - l1 and Hot Deck - l2. I also ran a Random Forest (RF) model using dataframes from each of these different data imputation methods, including a dataframe that simply removed samples that contained NaN values.

This is a comparison of the F1 score on validation data after implementing different forms of data imputation. For this data I found that *median imputation* was the most effective. 

<img width="472" alt="Screen Shot 2022-07-12 at 6 33 40 PM" src="https://user-images.githubusercontent.com/72525765/178629425-c1eebfa1-3854-4f21-acae-fbe9617a3898.png">

## Models

### Baseline Models 
Logistic Regression
- *max_iter:* 300
- *multi_class:* 'ovr'
- *C:* 62

Random Forest
- *depth:* 10
- *max_features:* 8
- *estimators:* 1500
- *min_samples_split:* 4

### More Complex Models
K-Nearest Neighbors
- *n:* 64
- *algo:* 'auto'
- *p:* 1.0
- *weights:* 'distance'

Feed Forward Neural Network
- *layers:* 8
- *activation:* ReLU
- *dropout:* 0.45
- *loss:* sparse_categorical_crossentropy
- *opimizer:* adam

## Results

After data cleaning, imputation, model training and recording the metrics, I produced the below table which summarizes my findings that kNN out performed the baseline RF and the Keras Sequential NN that I built and trained. 

Optimizing my kNN model was crucial to getting these results. Finding the exact value of n and p for the data was very important to getting good results and it was also an exhaustive search space. In the notebook section Hyper-parameter Searching I peform the search by retraining the kNN model and retesting to get f1 on each test model. The values of n and p in the above section of this readme are the optimized values for the split of data that I was using. 

<img width="469" alt="Screen Shot 2022-07-12 at 7 02 49 PM" src="https://user-images.githubusercontent.com/72525765/178635157-54e5a866-fd83-4b27-a640-dea04ea7e0ba.png">

## The code
The code notebook is here on the repo and can be used at your preference. I have many imputation and cleaning definitions that could be found useful with similar datasets. Enjoy the code!
