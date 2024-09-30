# Heart Disease Prediction

Helping doctors in identifying the patients carrying heart disease based on their genetic data and their lifestlye 

1. Gathering Data
2. Preprocessing
3. EDA and Statistical Test
4. Modelling
5. Hyperparameter tuning
6. Conclusion

1. Gathering Data

Data recieved is from a hospital database consists over data for 60k patients and their history of heart disease

2. Preprocessing 

Correlation test and missing value treatment is performed to ensure proper 

3. EDA and Statistical Test

Identifing feature which are significant to the model is done with the help of Chi Square test and T-test are performed.

On the existing data we are able to confirm features most importantly Gender and Smoking are significant feature and able to confirm that People who are female are likely to contract heart disease and if the patients who are smoking are likely to get heart disease

With the help of t-test we are confirm the numeric features which are important in identifying the heart disease. Age of the patient is an important feature which tell that patients who are over the age of 40 are likely to get heart disease

4. Modelling 

Dataset is preprocessing with the help of Standard Scaler to equalize the model from -1 to 1 and final data is run to all the classification model.

Precision is the preferred success metric used in this scenario.

Logistic Regression and Decision Tree have provided significant precision score and are used as the base model.

We have identified the feature importantance of the model and found the age, cholestrol and smoking are the major factors responsible for the heart disease which are explained when we performed EDA.


5. Hyper parameter tuning

Randomized CV and Grid CV are used to the existing base model with decision tree as the base, Modified the depth of the tree, number of root notes and the iteration and able to increase the accuracy and precision by 10% in the existing model

6. Conclusion

With the model been developed with Decision Tree. We can use the model to help doctor give a base estimate on patients who are likely to get heart disease and improve efficiency
