# Introduction
Out task is churn prediction of bank customers. Given hundreds of financial
behavioral data of bank customers, the goal is to predict whether a customer will eventually quit the
bank, i.e., no longer having transactions in the bank in the future. A snapshot of data is presented in Figure 1. There are 13 features whose meanings are correspondingly described in Table 1, and the prediction target is the “Exited” column.

<img width="502" alt="image" src="https://user-images.githubusercontent.com/79685898/169399852-c1e53fbd-d0e7-4853-b98a-47c88545aa44.png">



# Process

## 1.Discovery <br/>
### About this dataset
This is a dataset of financial behavioral data 
of bank customers, the goal is to predict whether
a customer will eventually quit the bank
### Baseline Model
20.6% of the customers will churn
### Feature
There are 13 features whose meanings are correspondingly described in Table 1, and the prediction target is the “Exited” column
### Train/test data(7:3)
There are 10000 sample datas, 7000 for training and 3000  for testing, the prediction score will be based on: Accuracy, Precision, recall and F-Score.


## 2.Exploratory Data Analysis <br/>
### Invalid Value for classificaion labels
Drop RowNumber、CustomerID、Surname
### Status relation with categorical variables
1.Majority of the data is from persons from France. <br/>
2.he proportion of female customers churning is also greater than that of male customers. <br/>
3.Interestingly, majority of the customers that churned are those with credit cards. <br/>
4.Unsurprisingly the inactive members have a greater churn. <br/>

![image](https://user-images.githubusercontent.com/79685898/169400571-a4006407-73bc-4a77-be9e-e3029c3e3d5f.png)


## 3.Data Preprocessing <br/>
### One-Hot Encoding
![image](https://user-images.githubusercontent.com/79685898/169400719-f1146503-5375-4eec-bd57-4444f243874f.png)
### Treatment for outliers
![image](https://user-images.githubusercontent.com/79685898/169400729-fde3ad51-d766-46c2-8486-d92b05ebb084.png)

## 4.Model Building <br/>
### Best Hyperparameters 
Training size = 2100   (Train size = 0.7, test size =0.3, random state =1 ) <br/>
GridSearchCV ( cv = 10 , scoring =‘accuracy’)

#### Logistic Regression
penalty = l2 ;  C=5 ; solver = liblinear 
#### SVM
C=5 ; gamma = 5; kernel = poly
#### KNN
Algorithm = auto ; n_neighbors = 10 ; weights = distance
#### Decision Tree
Criterion = gini ; max_leaf_nodes = 20; min_sample_split =2
#### Random Forests
Criterion = entropy ; max_features = 0.33;  n_estimators = 50
#### XGB
Gamma = 0.8, depth = 4, n_estimators = 100

### Feature importance score for random forest :
Age, NumofProducts, Balance, EstimatedSalary, CreditScore, Tenure
![image](https://user-images.githubusercontent.com/79685898/169401635-8a995008-efc3-4e5d-816e-f278d5513936.png)
### SMOTE
![image](https://user-images.githubusercontent.com/79685898/169401545-9b72ecce-d2c8-4ca0-a2e7-3865a90b18fd.png)
![image](https://user-images.githubusercontent.com/79685898/169401549-93bf26d3-f8f1-41a6-8394-a288d1c90146.png)
### Confusion matrix
#### Precision = 𝑇𝑃/(𝑇𝑃+𝐹𝑃)
#### Recall = 𝑇𝑃/(𝑇𝑃+𝐹𝑁)

![image](https://user-images.githubusercontent.com/79685898/169401860-4a97a1a5-6aef-4826-9bc4-724cdd47e4c9.png)
![image](https://user-images.githubusercontent.com/79685898/169401867-a9d4d1d0-e331-4322-a7a4-9e1e6c581568.png)
![image](https://user-images.githubusercontent.com/79685898/169401875-838aa700-9f9f-4416-b828-29cdce0333c0.png)

## 5.Communicate Results <br/>
### Discover key insights from database
1. Random forest can predict the churn with 80% accuracy, f-score = 0.62
2. Oversampling or undersampling method can solve imbalanced data.
3. Ensamble learning is good for classification problem.
### Support Business decision-making
1.  Customers between the ages of 40 and 65 were more likely to quit the bank.
2.  Find more data about customers, we can do PCA and get more predictive power feature.
