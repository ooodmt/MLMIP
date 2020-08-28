# Project 'Machine Learning for Medical Image Processing'
This repository contains code we used to set up, train and evaluate our neural networks, as well as implemented explanation techniques. We also provide instructions on how to try our code. Everything was done as part of a project at Technical University of Berlin.

## Content
- **Contributors**
- **Objective**
- **Results**
- **Combined model**
- **Dataset**
- **How to run our code**

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

After training, gradCAM and LIME were employed to look at regions of the image that contributed to the outcome of model's prediction. Below is example of explanation for prediction made by EfficientNet produced by gradCAM for 3 diseases with highest probability.

#### Original image
![Original image](https://raw.githubusercontent.com/ooodmt/MLMIP/master/sample_xray.jpg)

#### Resulting gradCAM for top-3 labels
![Original image](https://raw.githubusercontent.com/ooodmt/MLMIP/master/sample_gradCAM.jpg)

Overall inspected models tend to consider relevant regions of input space more often than irrelevant in case of correct predictions. However it is not happening consistently and big fraction of correct predictions cannot be attributed to a model's ability to detect true pathologies from image. Sometimes the predictions of models are influenced by spurious correlations or are simply random.

### Combined model
Combined model is a set of several CNNs with classification layers cut off and connected to a shared classification layer. See figure below.

![Combined model](https://raw.githubusercontent.com/ooodmt/MLMIP/master/combined_mod.jpg)


### Dataset
For this project we chose [CheXpert](https://stanfordmlgroup.github.io/competitions/chexpert/) dataset with over 200,000 images. Since original version contains labels indicating uncertainty in findings, for the purpose of efficient training we decided to replace corresponding "-1" labels with random numbers drawn from a uniform distribution in range [0.55, 0.85] as done by one of the CheXpert top scoring contributors.

### Some remarks
Evaluation was done on 5 labels out of 14, since the test set consists only of 207 records, where some diseases are not present, making computation of AUC score impossible.
Due to limited computational resources (one GPU allocated by project organisers) only compact architectures were possible to train. Also in explanation part these constraints played a role: it was not possible to run LIME on EfficientNet and combined model due to "CUDA Out of Memory Error", although the method itself is model agnostic. 

### How to try our code
#### Preliminary
In order for the code to work properly ensure you have CheXpert dataset downloaded and the structure of the folder is as shown below.
~~~
.  
└───data  
|   └───chexpert  
|       └───v1.0  
|       │   │   train.csv  
|       │   │   valid.csv  
|       │   └───train  
|       │   └───valid  
|       └───v1.0-small  
|           │   train.csv  
|           │   valid.csv  
|           └───train  
|           └───valid   
~~~

In the notebook provide a link either to v1.0 or v1.0-small by setting value of variable *data_path*.

#### Stepwise instructions
 1. Download state dictionaries for networks [here](https://drive.google.com/drive/folders/1M_U0vUwcOTzro_qQh11bIGQk5nsqm9zT?usp=sharing).
 2. Set up virtual environment in your jupyter notebook and download required packages (see what's imported).
 3. Set up path variables at the beginning of the notebook that you're about to run.
 4. Execute the code.


