# Fraud Detection with Unknown Features

*Yi Huang*  

## File Description  
* Ipynb file:  
	- [EDA.ipynb](https://github.com/yihuang1995/Fraud_Detection_with_Unknown_Features/blob/main/EDA.ipynb)  
	- [Final_Project_model_code.ipynb](https://github.com/yihuang1995/Fraud_Detection_with_Unknown_Features/blob/main/Final_Project_model_code.ipynb)  
* Data:  
	- [creditcard_down.csv](https://github.com/yihuang1995/Fraud_Detection_with_Unknown_Features/blob/main/creditcard_down.csv) 
* Presentation:  
	- [ml_lab_ppt.pptx](https://github.com/yihuang1995/Fraud_Detection_with_Unknown_Features/blob/main/ml_lab_ppt.pptx)
* Others:   
	- [images](https://github.com/juliafeec/tmdb/tree/master/images)  

## Goal
Fraud detection with unknown features

Fraud detection is a set of activities undertaken to prevent money or property from being obtained through false pretenses, which is a essentail topic for financial companies. Machine learning is a efficient way to detecte fraud behaviors. For this dataset, we are using definition-unknown features to classify the fraud/non-fraud data.   
 
## Data Description
**Base Dataset**:  
<https://www.kaggle.com/mlg-ulb/creditcardfraud>

The original data set's size is over 150M, in order to fulfill the requirement of the course project, I extracted over 5000 rows of the data to build the model. The dataset has 30 features, V1-V28 are unknown features, Time and Amount are the only two features with specific definition.


## Feature Engineering

+ **PCA**:  
	PCA is a method to reduce the dimension of all features. Since there are 28 unknown features, I want to explore whether PCA helps.
	
+ **Log-transform**:  
	For all columns, I perform log-transformation, and calculate the correlation with y. Columns with increased correlation will be selected to perform log column transformation.

## Model

All models' hyperparameters are selected using Randomized Search CV methods. 80% of the data are used to train the model.

+ **Model1**: Standard Scaler + PCA + SMOTE + Random Forest 
+ **Model2**: Log-transform + SMOTE + Gradient Boosting


## Modeling results on test set

| Metrics                  | Model1 (rf)             | Model2 (GB)   |
| :----------------------: | :---------------------: | :-----------: |
| Balanced Accuracy        | 0.932                   | 0.942         |  
| F1 Score                 | 0.909                   | 0.921         |
| Precision                | 0.955                   | 0.956         |
| **Recall**               | **0.867**               | **0.888**     |




## Conclusion

+ **Best Model**:   
	Feature Selection + GradientBoosting model.   

+ **Model conclusion**:  
	Feature Selection + GradientBoosting model is slightly better than the PCA + RandomFrorest model. One reason might be that PCA reduces the information model can get from the data. Another reason is GradientBoosting algorithm might have better prediction power than the RandomForest..   
	
+ **Business conclusion**:   
	This is a fraud detection problem, we care the recall of the model, which means that how many fraud cases can be found from the model. 0.89 recall score means a pretty good model. If we are working as a vendor for our client, some features might be encrypted and unknown the true meaning of it, it is a good practice to know how to do feature engineering on those features.

+ **Next Steps**:  
	+ Deeper feature engineering: more transformation, combining features, add new features from original features
	+ More complex model: Ensamble model, Stacked model
