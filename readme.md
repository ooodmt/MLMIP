# Project 'Machine Learning for Medical Image Processing'
This repository contains code we used to set up, train and evaluate our neural networks, as well as implemented explanation techniques. We also provide instructions on how to try our code. Everything was done as part of a project at Technical University of Berlin.
### Contributors
* Shiva Banasaz Nouri (presentation, data preprocessing)
* Alex Serbin (explanation techniques, data exploration)
* Babak Sistani Zadeh Aghdam (presentation, data preprocessing)
* Mingzhi Wang (model training and evaluation)

### Objective
Train several convolutional neural networks on CheXpert dataset for multilabel classification and take use existing explanation techniques to visualize parts of input space relevant to network's predictions.

### Results
DensetNet-121, EfficientNet and combined model (described below) were trained. The resulting AUC scores are given below.

Model | AUC score
------------ | -------------
DenseNet-121 | 0.81
Combined model | 0.84
EfficientNet | 0.88

After training gradCAM and LIME were employed to look at regions of the image that led to certain probability assignments. Below is example of explanation for prediction produced by gradCAM for 3 diseases with highest probability.

#### Original image
![Original image](https://raw.githubusercontent.com/ooodmt/MLMIP/master/sample_xray.jpg)

#### Resulting gradCAM for top-3 labels
![Original image](https://raw.githubusercontent.com/ooodmt/MLMIP/master/sample_gradCAM.jpg)

Overall inspected models tend to consider relevant regions of input space more often than irrelevant in case of correct predictions. However it is not happening consistently and big fraction of correct predictions cannot be attributed to a model's ability to detect true pathologies from image. Sometimes the predictions of models are influenced by spurious correlations or are simply random.

### Description
Combined model is a set of several CNNs without their own classification layers, connected to a shared claassification layer. See figure below.

### Dataset
For this project we chose CheXpert dataset with over 200,000 images. Since original version contains labels indicating uncertainty in findings, for the purpose of efficient training we decided to replace corresponding "-1" labels with random numbers drawn from a uniform distribution in range [0.55, 0.85] as done by one of the CheXpert top scoring contributors.

### Remarks
Evaluation was done on 5 labels out of 14, since the test set consists only of 207 records, where some diseases are not present, making computation of AUC score impossible.

Also due to limited computational resources (one GPU allocated by project organisers) only compact architectures were possible to train. Also in explanation part these constraints played a role: it was not possible to run LIME on EfficientNet and combined model due to "CUDA Out of Memory Error", although the method itself is model agnostic. 




