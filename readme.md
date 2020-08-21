# Machine Learning for Medical Image Processing: group Igloo
### Technical University of Berlin
This repository contains code we used to set up, train and evaluate our neural networks, as well as to implement explanation techniques. We also provide instructions on how to try our code 

### Project objective
Train several convolutional neural networks on CheXpert dataset for multilabel classification of 14 diseases and take advantage of existing explanation techniques to understand network's predictions.

### Results
We trained DensetNet-169, EfficientNet and combined model (described below). The resulting AUC scores are given below.

Model | AUC score
------------ | -------------
DenseNet-169 | 0.81
EfficientNet | 0.84
Combined model| 0.88

After training we employed gradCAM and LIME to understand causes of network's probability assignments. Below is the example of explanation for prediction produced by gradCAM for 3 with highest probability.

#### Original image
![Original image](https://raw.githubusercontent.com/ooodmt/MLMIP/master/sample_xray.jpg)

#### Resulting gradCAM for top-3 labels
![Original image](https://raw.githubusercontent.com/ooodmt/MLMIP/master/sample_gradCAM.jpg)


contributors
structure of repository
how to try our code
dataset
results



