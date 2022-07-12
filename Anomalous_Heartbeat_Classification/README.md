# Arrhythmia Detection and Classification

This project was done for The University of Washington's Professional Master's Program AI and Healthcare course taught by Dr. Karthik Mohan, and it was a partner project.

## Introduction

Data preprocessing, data generation, and model training and comparison, including a SOTA CNN model, for Heartbeat classification, specifically class 'A' for Arrythmia. A Test set F1 of 0.964 was achieved using the SOTA CNN with 1 feature, MLII readings.

## Dataset

The Dataset can be found here in the mitbih_databse directory. The data folder contains 44 csv files with corresponding txt files to annotate the csv files. Using the annotated R-peaks from the txt files, the csv files could be broken down into individual heartbeats for each patient. However, only 42 of the patients had the 'MLII' ECG reading so we opted to use just that one feature for the majority of the work.

The data was preprocessed into a dataframe of 98,312 x 360. Here the 98,132 refers to the total number of heartbeats we extracted from the 42 patients, and 360 represents the MLII values for each heartbeat. Heartbeats are created by taking 180 values left of the R-peak and 179 values right of the R-peak, this created a 360-d vector which represented one ECG sensor reading for one heartbeat. This database was collected using a two-channel ambulatory ECG between 1975 and 1979. These R-peaks have been hand annotated by cardiologists after digitization. 

To ensure that each patient was normalized with respect to their own heartbeat ECG data, we normalized by patient before concatenating the heartbeats of a single patient to the larger dataframe with all the patients. 

## Data Imbalance

Since a normal heartbeat is significantly more common to read when taking the ECG of a patient, this created a large dataset imbalance as shown below. Notice there are 6 classes, 'N' representing normal heartbeat.

![class_imbalance_bar](https://user-images.githubusercontent.com/72525765/178570295-b89dda09-f9e4-4189-a562-94b8d27fd7fb.png)

## Autoencoders for Data Generation

To overcome the massive data imbalance presented in the dataset, my partner and I  tried a basic autoencoder and a variational autoencoder, and found very comparable results between the two. 

Using the Autoencoder, we boosted the samples in the 5 classes that were low. Still, each class had about 3/5 the samples of the N class. 

![class_imbalance_bar_ae](https://user-images.githubusercontent.com/72525765/178571253-d87559dc-3560-
4e70-99d5-9bf245e97367.png)
![ae_results](https://user-images.githubusercontent.com/72525765/178572200-9da593bd-69b9-4241-a9f4-c179987e66bb.PNG)


Using the Variational Autoencoder, we also boosted the low classes, but this time leveled the classes out with the N class. 

![class_imbalance_bar_vae](https://user-images.githubusercontent.com/72525765/178571755-da686501-1fbc-4ecd-bc75-a2f3f0237b8e.png)
![vae_results](https://user-images.githubusercontent.com/72525765/178572212-1d3ca8d7-c5b8-45a1-b431-cca9ad40436d.PNG)



## Models

## Training

## Results
