# Personalized cancer diagnosis
## 1. Business Problem
### 1.1. Description

Source: https://www.kaggle.com/c/msk-redefining-cancer-treatment/

Data: Memorial Sloan Kettering Cancer Center (MSKCC)

Download training_variants.zip and training_text.zip from Kaggle.

#### Context:

Source: https://www.kaggle.com/c/msk-redefining-cancer-treatment/discussion/35336#198462

#### Problem statement :

Classify the given genetic variations/mutations based on evidence from text-based clinical literature.

## 2. Machine Learning Problem Formulation
### 2.1. Data
### 2.1.1. Data Overview

    Source: https://www.kaggle.com/c/msk-redefining-cancer-treatment/data
    We have two data files: one conatins the information about the genetic mutations and the other contains the clinical evidence (text) that human experts/pathologists use to classify the genetic mutations.
    Both these data files are have a common column called ID


## 2.2. Mapping the real-world problem to an ML problem
### 2.2.1. Type of Machine Learning Problem

There are nine different classes a genetic mutation can be classified into => Multi class classification problem
### 2.2.2. Performance Metric

Source: https://www.kaggle.com/c/msk-redefining-cancer-treatment#evaluation

Metric(s):

    Multi class log-loss
    Confusion matrix

### 2.2.3. Machine Learing Objectives and Constraints

Objective: Predict the probability of each data-point belonging to each of the nine classes.

Constraints:

    Interpretability
    Class probabilities are needed.
    Penalize the errors in class probabilites => Metric is Log-loss.
    No Latency constraints.

## 2.3. Train, CV and Test Datasets

Split the dataset randomly into three parts train, cross validation and test with 64%,16%, 20% of data respectively

# 3. Exploratory Data Analysis

## 3.1. Reading Data
### 3.1.1. Reading Gene and Variation Data
### 3.1.2. Reading Text Data
### 3.1.3. Preprocessing of text

### 3.1.4. Test, Train and Cross Validation Split
#### 3.1.4.1. Splitting data into train, test and cross validation (64:20:16)
#### 3.1.4.2. Distribution of y_i's in Train, Test and Cross Validation datasets

## 3.2 Prediction using a 'Random' Model

In a 'Random' Model, we generate the NINE class probabilites randomly such that they sum to 1.

## 3.3 Univariate Analysis

### 3.2.1 Univariate Analysis on Gene Feature


# 4. Machine Learning Models
## 4.1. Base Line Model
### 4.1.1. Naive Bayes
Log Loss : 1.153235894590452
Number of missclassified point : 0.38345864661654133

## 4.2. K Nearest Neighbour Classification
Log loss : 1.0324353214410276
Number of mis-classified points : 0.36466165413533835

### 4.3. Logistic Regression
### 4.3.1. With Class balancing
Log loss : 1.043318050124558
Number of mis-classified points : 0.3458646616541353
### 4.3.2. Without Class balancing
Log loss : 1.062988230671672
Number of mis-classified points : 0.3533834586466165
## 4.4. Linear Support Vector Machines
Log loss : 1.076836039361882
Number of mis-classified points : 0.3458646616541353
## 4.5 Random Forest Classifier
### 4.5.1. Hyper paramter tuning (With One hot Encoding)
Log loss : 1.1978667267936522
Number of mis-classified points : 0.39473684210526316
### 4.5.3. Hyper paramter tuning (With Response Coding)
Log loss : 1.3352069773071837
Number of mis-classified points : 0.4943609022556391

## 4.7 Stack the models
Log loss (train) on the stacking classifier : 0.5386754023282136
Log loss (CV) on the stacking classifier : 1.138717562146062
Log loss (test) on the stacking classifier : 1.1742087492677697
Number of missclassified point : 0.38646616541353385

### 4.7.3 Maximum Voting classifier
Log loss (train) on the VotingClassifier : 0.8329702627479129
Log loss (CV) on the VotingClassifier : 1.1887678593349613
Log loss (test) on the VotingClassifier : 1.2061284826287209
Number of missclassified point : 0.3849624060150376

# Logistic regression with CountVectorizer Features, including both unigrams and bigrams
Log loss : 1.1025061826224287
Number of mis-classified points : 0.36278195488721804

# adding Variation Feature,Text Feature to improve the performance
Log loss : 0.9976654523552164
Number of mis-classified points : 0.3233082706766917
# Conclusion
After some feature engineering we manage to decrease the log loss below < 1. We can adopt more feature enginnering methods and reduce the log loss furhermore.

