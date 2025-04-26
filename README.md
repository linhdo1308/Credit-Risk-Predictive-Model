# Home-Credit-Risk-Kaggle

This is a project from a featured prediction competition hosted by Home Credit on [Kaggle](https://www.kaggle.com/competitions/home-credit-default-risk/overview) conducted by me and three other teammates. The purpose of this project is to create a predictive model on clients’ ability of loan repayments.

In this notebook, I conduct exploratory data analysis and feature engineering on additional datasets (bureau.csv, bureaubalance.csv, installmentpayments.csv, creditcardbalance.csv). We spend a long time on adjusting these feature engineer and selection to improve the models. However, it turns out that most of the most important predictors lie in the main dataset (application_train.csv) and including unnecessary features will introduce noise to the model. Therefore, our final model only keeps the most important features from the main dataset and previous_application which adds more information for applicants without credit scores. 

In conclusion, for this type of prediction problem, the most critical factors for improving model performance are incorporating meaningful features and applying effective feature engineering.

## 1. An Overview of the Project
### a. Business Problem

Home Credit focuses on delivering greater access to financial services through financial inclusion efforts across markets, including the unbanked. With insufficient or non-existent credit history, it is hard for them to receive loans from financial institutions. However, in order to guarantee a positive and safe borrowing experience, Home Credit needs to predict their ability of loan repayments with data.

### b. Analytical Methodology

Default risk prediction will be generated using a supervised machine learning classification model. Historical loan application data will be split into two sets, 80% for training and 20% for test. My team will build the model based on the trained dataset and test its performance on the test set. The model will analyze factors like applicant demographics, credit history, past loan performance and repayment behavior to predict the chances of clients’ default on loans. Throughout the project, we try different feature engineering and predictive models including logistic regression, random forest, decision tree and CATBOOST. 

In general, our best model (CATBOOST) achieves an overall 70% accuracy and a balanced predictability between defaulters & non-defaults.

## 2. Business Insights and Recommendations
### a. Business Insights
- Younger people tend to have more problems on loan repayment.
- Applicants who change their number within 12 months are more likely to default.
- Highest default risk is observed in the population with the lowest credit score (from 0 - 0.4). Applicants in this group will increase the likelihood of default by 65%. Interestingly, even those without credit scores shows moderate risk since they increase the probability of default by 50%.

### b. Recommendations
- Develop personalized loan packages:

Leverage customer data and predictive analytics to tailor loan offers with customized interest rates based on each borrower’s predicted default probability. This approach not only enhances customer satisfaction by providing fair, personalized rates but also improves the bank’s risk management and portfolio performance.

- Marketing products to the target unbanked customer:

With a solid understanding of the target customer, the bank should focus its marketing resources on this segment. Additionally, the marketing team should investigate the group’s pain points and behaviors to tailor campaigns that effectively attract them.
