# Breast Cancer Prediction with Deep Learning and Explainable Models

This project was done for The University of Washington's Professional 
Master's Program AI and Healthcare course taught by Dr. Karthik Mohan.

## Introduction

This is a binary classification problem of which I created a dense feed forward neural network which achieved the f1 score of 0.954 on test set, and an explainable model in an attempt to create an explainable model for the deep network black box problem.

## Dataset

For this assignment I chose to work with the Breast Cancer Prediction Dataset from Kaggle, which can be found here: https://www.kaggle.com/datasets/merishnasuwal/breast-cancer-prediction-dataset

This dataset is a csv file and when read into my Python notebook takes the dataframe below. These values are unnormalized here, for my ML models I normalized them. The feature set is shown below, this data has 5 features to predict the cancerous lumps, with the diagnosis taking on 0 or 1.

<img width="551" alt="Screen Shot 2022-07-12 at 7 30 00 PM" src="https://user-images.githubusercontent.com/72525765/178638162-b502c5e0-c7a1-47d0-9322-a7c85ee2d58c.png">

## Models

### Explainable Models
Decision Tree
- *criterion:* entropy
- *max_depth:* 6

Random Forest
- *depth:* 10
- *estimators:* 25
- *min_samples_split:* 3

### Non-Explainable Models
Dense Feed Forward Neural Network
- *layers:* 5 
- *activations:* ReLU
- *loss:* binary cross entropy
- *optimizer:* adam
- *trained for epochs:* 35

## Results

The NN trained for the 35 epochs and was able to achieve 0.9538 f1 score on test set, while the explainable models were only able to achieve 0.9355 and 0.9333 for DT and RF respectively. This difference was actually very promising, as there were only a handful of samples that could be differently classified between the explainable and non explainable models, making the explainable models more convincing. 

<img width="391" alt="Screen Shot 2022-07-12 at 7 46 55 PM" src="https://user-images.githubusercontent.com/72525765/178639996-17373801-74d0-4bda-a8e4-0b5cef63216b.png">

I used a previous code for DT explainability which generates a list of directions taken at each DT node until eventually the leaf node is found. This outputs the feature name and threshold at the node, the value of the feature we have and the direction taken. These produce a visual and textual explanation of the DT path, and since the difference in f1 is so small between the DT and the NN, this can also be used to explain the prediction of the NN. 

## The code
The code and intermediary results, as well as two more sections of results are in the notebook in this repo. Enjoy the code and feel free to download and play around with it!
