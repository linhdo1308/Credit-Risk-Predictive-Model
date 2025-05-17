# Credit Risk Predictive Model for Home Credit

This is a project from a featured prediction competition hosted by Home Credit on [Kaggle](https://www.kaggle.com/competitions/home-credit-default-risk/overview) conducted by me and three other teammates. The purpose of this project is to create a predictive model on clients’ ability of loan repayments.

## 1. An Overview of the Project
### a. Business Problem

Home Credit aims to expand financial access to unbanked customers. Lacking credit histories makes loan approvals challenging, so predictive models are used to assess their repayment ability and ensure responsible lending.

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

### 3. My contribution in the project
In this notebook, I conduct exploratory data analysis and feature engineering on additional datasets (bureau.csv, installmentpayments.csv, creditcardbalance.csv). 

Since bureau.csv is a time-series dataset on previous credits in Credit Bureau, I aggregate on SK_ID_CURR to join with the application_train dataset. Specifically, I conduct the following feature engineering:
- Number of active credits: the number of credit accounts that the applicant currently has. If the applicant has a high number of active credits, it could suggest they are under financial burden. In this case, we may doubt their ability to pay off the loans.
- Number of closed credits: the number of credit accounts that the applicant has paid off. If the applicant has a high number of closed credits (if paid off without default), it could suggest their ability to repay loans.
- Mean and Median DAYS_CREDIT_ENDDATE: the average loan term for the applicant. Long-term loans could indicate applicant's debt management over a long period of time
- Mean and Median REDIT_DAY_OVERDUE: the average number of days the applicant is overdue on their credit payments. High mean/median overdue days may indicate repayment struggles
- Mean and Median DURATION_OF_CREDIT: the average length of time an applicant has had a credit account or loan. A shorter credit duration might indicate a lack of experience with managing loans, or it might suggest financial stress if the borrower is taking out credit quickly to meet short-term needs.
- Mean and Median AMT_CREDIT_SUM: the average total amount of credit an applicant has taken out across all loans. A high mean/median total credit sum can indicate either the applicant has better financial standing or higher financial pressures, especially if they have trouble managing their payments across multiple accounts
- Mean and Median AMT_CREDIT_SUM_DEBT: the average total outstanding debt the applicant owes. If the mean or median debt amount is high, this indicates a burden of unpaid debts which is more prone to default.
I use both mean and median since mean is a better metric if the applicant has a low number of bureau credits, while median is a better metric if the applicant has a high  number of bureau credits.

Since creditcardbalance.csv is also a time-series data representing monthly balance snapshots of previous credit cards that the applicant has with Home Credit, I will aggregate it on SK_ID_PREV level. However, after examining the relationships between target variable and these featured engineering variables, I find that they don't have high correlation. Therefore, these variables will not be used in the models.

Specifically, I conduct the following feature engineering:
- Duration: the number of months the credit card has been used. A short duration may indicate that the applicant is inexperienced in credit management
- Mean and Median AMT_BALANCE: the amount owed on the credit card. High balances coupled with insufficient income or financial strain can suggest a borrower at risk of default
- Mean and Median AMT_CREDIT_LIMIT_ACTUAL: the actual credit limit available to the borrower on the credit card. If the borrower has a high limit but consistently high balances, they may be over-leveraged, more prone to default.
- Mean and Median AMT_DRAWINGS_OTHER_CURRENT: the amount spent on other current purchases or withdrawals. High spending can indicate the borrower is heavily reliant on credit.
- Mean and Median AMT_DRAWINGS_POS_CURRENT: total amount spent using the Point-of-Sale (POS) system or for purchases at physical stores. Higher spending at POS can indicate a pattern of over-expenditure, especially if the borrower is unable to repay the amount within the month
- Mean and Median SK_DPD: the number of days the borrower is overdue on their credit card payments. It can be a strong predictor since a high number of days overdue can suggest the applicant has difficulty to repay the loan.
- Mean and Median SK_DPD_DEF: the number of days past due when a borrower has defaulted on a payment
- Max CNT_INSTALMENT_MATURE_CUM: if the applicant has a large number of matured installments, it could indicate a long-term history of missed or delayed payments. This may be an indicator of loan default.

Since installment payment dataset represents repayment history for the previously disbursed credits in Home Credit, I will aggregate it on SK_ID_PREV level. Specifically, I conduct the following feature engineering:
- max_num_instalment_version: maximum number of installment versions. if a borrower frequently modifies or extends the number of installments in their loan repayment schedule, it can indicate difficulties in repaying the loan within the original terms
- total_instalment_number: total number of installment payments
- PAY_ONTIME: whether the payment is made ontime (1 - ontime, 2 - early, 3 - late)
- ENOUGH_PAY: whether the full amount is paid off (1 - the amount is paid in full, 2 - the amount is paid less, 3 - the amount is paid more)

### 4. What are the difficulties and learning points from the project?
Throughout the project, our team spends a lot of time on feature engineering and improving model performance. At first, although we aggregate features from extra datasets, the model performs poorly and only a few of these variables are selected as strong predictors for the default problem. Furthermore, all model suggests bias to the majority class due to class imbalance issues even though we already downsampled and scaled the data to prevent bias.

However, it turns out that most of the most important predictors lie in the main dataset (application_train.csv) and including unnecessary features will introduce noise to the model. Additionally, conducting feature engineering on the extra data significantly increases the model’s running time. Therefore, our final model only keeps the most important features from the main dataset and previous_application which adds more information for applicants without credit scores. 

In conclusion, for this type of prediction problem, the most critical factors for improving model performance are incorporating meaningful features and applying effective feature engineering. Strong feature engineering, guided by domain knowledge of the business problem, can significantly enhance the model's ability to capture relevant patterns and deliver more accurate predictions.
