# Arrhythmia Detection and Classification

This project was done for The University of Washington's Professional Master's Program AI and Healthcare course taught by Dr. Karthik Mohan, and it was a partner project.

## Introduction

Data preprocessing, data generation, and model training and comparison, including a SOTA CNN model, for Heartbeat classification, specifically class 'A' for Arrythmia. A Test set F1 of 0.964 was achieved using the SOTA CNN with 1 feature, MLII readings.

## Dataset

The Dataset can be found here in the mitbih_databse directory. The data folder contains 44 csv files with corresponding txt files to annotate the csv files. Using the annotated R-peaks from the txt files, the csv files could be broken down into individual heartbeats for each patient. However, only 42 of the patients had the 'MLII' ECG reading so we opted to use just that one feature for the majority of the work.

The data was preprocessed into a dataframe of 98,312 x 360. Here the 98,132 refers to the total number of heartbeats we extracted from the 42 patients, and 360 represents the MLII values for each heartbeat. Heartbeats are created by taking 180 values left of the R-peak and 179 values right of the R-peak, this created a 360-d vector which represented one ECG sensor reading for one heartbeat. This database was collected using a two-channel ambulatory ECG between 1975 and 1979. These R-peaks have been hand annotated by cardiologists after digitization. 

To ensure that each patient was normalized with respect to their own heartbeat ECG data, we normalized by patient before concatenating the heartbeats of a single patient to the larger dataframe with all the patients. 

Examples of Heartbeats from each class parsed during preprocessing:
![N1](https://user-images.githubusercontent.com/72525765/178573451-572cd337-36bf-4eb1-bc46-b31593ec725d.PNG)
![L3](https://user-images.githubusercontent.com/72525765/178573450-99de9978-9371-49f2-b41f-252ad2b4ac19.PNG)
![R2](https://user-images.githubusercontent.com/72525765/178573443-2c830248-e5fe-4aab-a88c-853e7fe9649a.PNG)
![A2](https://user-images.githubusercontent.com/72525765/178573449-281845af-0082-4c9f-a5d0-31e553ec08b9.PNG)
![V3](https://user-images.githubusercontent.com/72525765/178573446-f1c7b4d1-08b7-4e04-83f8-d6c8dbb53587.PNG)
![U3](https://user-images.githubusercontent.com/72525765/178573445-a25992ce-d74e-4aac-b722-fa6ba19d394f.PNG)

## Data Imbalance

Since a normal heartbeat is significantly more common to read when taking the ECG of a patient, this created a large dataset imbalance as shown below. Notice there are 6 classes, 'N' representing normal heartbeat.

![class_imbalance_bar](https://user-images.githubusercontent.com/72525765/178570295-b89dda09-f9e4-4189-a562-94b8d27fd7fb.png)

## Autoencoders for Data Generation

To overcome the massive data imbalance presented in the dataset, my partner and I  tried a basic autoencoder and a variational autoencoder, and found very comparable results between the two. 

Using the Autoencoder, we boosted the samples in the 5 classes that were low. Still, each class had about 3/5 the samples of the N class. 

![class_imbalance_bar_ae](https://user-images.githubusercontent.com/72525765/178571253-d87559dc-3560-4e70-99d5-9bf245e97367.png)

Using the Variational Autoencoder, we also boosted the low classes, but this time leveled the classes out with the N class. 

![class_imbalance_bar_vae](https://user-images.githubusercontent.com/72525765/178571755-da686501-1fbc-4ecd-bc75-a2f3f0237b8e.png)

Shown below are the tables for the metrics used to compare each model, as you can see the basic autoencoder actually produces better end results than the variational autoencoder did.

![ae_results](https://user-images.githubusercontent.com/72525765/178572200-9da593bd-69b9-4241-a9f4-c179987e66bb.PNG)
![vae_results](https://user-images.githubusercontent.com/72525765/178572212-1d3ca8d7-c5b8-45a1-b431-cca9ad40436d.PNG)

## Denoising

We also implemented a feature for data denoising, enabling us to clean each signal so that the deep learning algorithms focus on the big picture of the data fluctuations and not the small jitters that don't contribute to type of heartbeat.

![noise1](https://user-images.githubusercontent.com/72525765/178575330-7cf91311-28f8-47e2-9e81-945e8f0d29ed.PNG)
![noiseless1](https://user-images.githubusercontent.com/72525765/178575327-2046b793-9147-4dca-84a5-c1cfca719f79.PNG)

## Models

Random Forest:
- *depth:* 20
- *estimators:* 25
- *min_samples_split:* 2

Feed Forward Neural Network:
- *API:* Keras Sequenial Model
- *Layer Count:* 6
- *Activation:* ReLU
- *Dropout:* 0.6
- *Loss:* Categorical Cross Entropy
- *Optimizer:* Adam
- *Target:* Label Binarizer of the 6 classes N,L,R,A,V,U

We used the CNN architecture proposed in the paper “X. Xu and H. Liu, "ECG Heartbeat
Classification Using Convolutional Neural Networks," in IEEE Access, vol. 8, pp. 8614-8619,
2020, doi: 10.1109/ACCESS.2020.2964749”.
- *API:* PyTorch
- *1D-Convolutional Layers:* 4
- *Pooling Layers:* 2
- *Linear Layers:* 3
- *Loss:* Cross Entropy
- *Optimizer:* Adam

## Training
With the above specs for the NN and CNN, we completed training for the NN and CNN for 9 and 8 epochs respectfully. The CNN had much smoother descent for accuracy and loss curves and proved better to use than the NN. 

![nn_train_loss_acc](https://user-images.githubusercontent.com/72525765/178577326-7bf1f0be-6987-4ecf-a4d2-263adc0ffc40.PNG)
![cnn_train_loss_acc](https://user-images.githubusercontent.com/72525765/178577347-14b86009-5f5d-47bc-8a74-f4adb4e5e3d9.PNG)

## Results

To measure the correctness of the model we took a look at the metrics by class: precision, recall and f1. With upsampling we were able to achieve a much higher accuracy for class 'A', Arrythmic heartbeat, but still significantly worse than other classes. The CNN paper claims 99.4% accuracy where we achieved 97% accuracy. 

![metrics_by_class_NN](https://user-images.githubusercontent.com/72525765/178577557-de8b595a-2570-450e-92be-42c935a1fa2b.PNG)

After creating a new dataframe with only patients that have both MLII and V1 readings, we were able to achieve a higher f1 score with the CNN than before using only one feature, namely MLII. 

![mlii_v1](https://user-images.githubusercontent.com/72525765/178578082-339a0aca-8fa0-4637-b1aa-1908c096199b.PNG)

## The code

Please check out the notebook for more intermediary results and full preprocessing, model creation, training and analysis functions / cells. Enjoy!

