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
### 1.2. Source/Useful Links

Some articles and reference blogs about the problem statement

    https://www.forbes.com/sites/matthewherper/2017/06/03/a-new-cancer-drug-helped-almost-everyone-who-took-it-almost-heres-what-it-teaches-us/#2a44ee2f6b25
    https://www.youtube.com/watch?v=UwbuW7oK8rk
    https://www.youtube.com/watch?v=qxXRKVompI8

### 1.3. Real-world/Business objectives and constraints.

    No low-latency requirement.
    Interpretability is important.
    Errors can be very costly.
    Probability of a data-point belonging to each class is needed.

## 2. Machine Learning Problem Formulation
### 2.1. Data
### 2.1.1. Data Overview

    Source: https://www.kaggle.com/c/msk-redefining-cancer-treatment/data
    We have two data files: one conatins the information about the genetic mutations and the other contains the clinical evidence (text) that human experts/pathologists use to classify the genetic mutations.
    Both these data files are have a common column called ID

    Data file's information:
        training_variants (ID , Gene, Variations, Class)
        training_text (ID, Text)

#### 2.1.2. Example Data Point

training_variants

ID,Gene,Variation,Class
0,FAM58A,Truncating Mutations,1
1,CBL,W802*,2
2,CBL,Q249E,2
...

training_text

ID,Text
0||Cyclin-dependent kinases (CDKs) regulate a variety of fundamental cellular processes. CDK10 stands out as one of the last orphan CDKs for which no activating cyclin has been identified and no kinase activity revealed. Previous work has shown that CDK10 silencing increases ETS2 (v-ets erythroblastosis virus E26 oncogene homolog 2)-driven activation of the MAPK pathway, which confers tamoxifen resistance to breast cancer cells. The precise mechanisms by which CDK10 modulates ETS2 activity, and more generally the functions of CDK10, remain elusive. Here we demonstrate that CDK10 is a cyclin-dependent kinase by identifying cyclin M as an activating cyclin. Cyclin M, an orphan cyclin, is the product of FAM58A, whose mutations cause STAR syndrome, a human developmental anomaly whose features include toe syndactyly, telecanthus, and anogenital and renal malformations. We show that STAR syndrome-associated cyclin M mutants are unable to interact with CDK10. Cyclin M silencing phenocopies CDK10 silencing in increasing c-Raf and in conferring tamoxifen resistance to breast cancer cells. CDK10/cyclin M phosphorylates ETS2 in vitro, and in cells it positively controls ETS2 degradation by the proteasome. ETS2 protein levels are increased in cells derived from a STAR patient, and this increase is attributable to decreased cyclin M levels. Altogether, our results reveal an additional regulatory mechanism for ETS2, which plays key roles in cancer and development. They also shed light on the molecular mechanisms underlying STAR syndrome.Cyclin-dependent kinases (CDKs) play a pivotal role in the control of a number of fundamental cellular processes (1). The human genome contains 21 genes encoding proteins that can be considered as members of the CDK family owing to their sequence similarity with bona fide CDKs, those known to be activated by cyclins (2). Although discovered almost 20 y ago (3, 4), CDK10 remains one of the two CDKs without an identified cyclin partner. This knowledge gap has largely impeded the exploration of its biological functions. CDK10 can act as a positive cell cycle regulator in some cells (5, 6) or as a tumor suppressor in others (7, 8). CDK10 interacts with the ETS2 (v-ets erythroblastosis virus E26 oncogene homolog 2) transcription factor and inhibits its transcriptional activity through an unknown mechanism (9). CDK10 knockdown derepresses ETS2, which increases the expression of the c-Raf protein kinase, activates the MAPK pathway, and induces resistance of MCF7 cells to tamoxifen (6). ...
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

Q1. Gene, What type of feature it is ?

Ans. Gene is a categorical variable

Q2. How many categories are there and How they are distributed?


Q3. How to featurize this Gene feature ?

Ans.there are two ways we can featurize this variable check out this video: https://www.appliedaicourse.com/course/applied-ai-course-online/lessons/handling-categorical-and-numerical-features/

    One hot Encoding
    Response coding

We will choose the appropriate featurization based on the ML model we use. For this problem of multi-class classification with categorical features, one-hot encoding is better for Logistic regression while response coding is better for Random Forests.


Q4. How good is this gene feature in predicting y_i?

There are many ways to estimate how good a feature is, in predicting y_i. One of the good methods is to build a proper ML model using just this feature. In this case, we will build a logistic regression model using only Gene feature (one hot encoded) to predict y_i.


Q5. Is the Gene feature stable across all the data sets (Test, Train, Cross validation)?

Ans. Yes, it is. Otherwise, the CV and Test errors would be significantly more than train error.

3.2.2 Univariate Analysis on Variation Feature

Q7. Variation, What type of feature is it ?

Ans. Variation is a categorical variable

Q8. How many categories are there?
Ans: There are 1933 different categories of variations in the train data, and they are distibuted as follows


Q9. How to featurize this Variation feature ?

Ans.There are two ways we can featurize this variable check out this video: https://www.appliedaicourse.com/course/applied-ai-course-online/lessons/handling-categorical-and-numerical-features/

    One hot Encoding
    Response coding

We will be using both these methods to featurize the Variation Feature


Q10. How good is this Variation feature in predicting y_i?

Let's build a model just like the earlier!
 Q11. Is the Variation feature stable across all the data sets (Test, Train, Cross validation)?

Ans. Not sure! But lets be very sure using the below analysis


Q. Is the Text feature stable across all the data sets (Test, Train, Cross validation)?

Ans. Yes, it seems like!
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

