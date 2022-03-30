# Credit Card Payment Model
## Introduction
Almost everyone uses a credit card in today's world.  Not everyone, however, pays off their credit card debts promptly–or at all. Because of this, we wanted to build models that would give credit card companies the ability to predict whether or not a cardholder will pay off their debt promptly and the percent of payments that they will likely miss.  
The data set we used to build and train our model comes from Kaggle (https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud).
The original data set contained over 777,000 rows and included customer ID, customer salary, customer age, card status, etc. For data cleaning, we renamed all of the columns to be more helpful, dropped the occupation column because of the missing rows, labeled encoded all of the objects, and only used clients who had been cardholders for 6 months or greater. For simplicity and ease of analysis, we created summary statistics for each cardholder, such as the percentage of payments they have missed, amount of times they have appeared in the data set, and their mode card status.

## Data Features Explanations
Here is what each column represents::
- **id**: client number
- **gender**: gender of client
- **has_car**: does client own a car
- **has_property**: does client have property
- **num_child**: number of children client has
- **salary**: annual salary of client in dollars
- **income_type**: how client gets their income
- **edu_type**: highest level of education obtained by client
- **married_type**: marital status of client
- **property_type**: type of property client owns
- **age_days**: age of client in days
- **days_employed**: amount of days client has been employed (negative means they have been unemployed for the absolute value of that number. example: -46 means they have been unemployed for 46 days)
- **has_cell**: does client own a cell phone
- **has_work_phone**: does client own a work phone
- **has_house_phone**: does client have a house phone
- **has_email**: does client have an email address
- **num_fam_members**: number of family members in household (property)
- **card_status_months_ago**: (used with "**card_status**") the amount of months that have elapsed since the values in "**card_status**" have been obtained

## Card Status Explanation
**card_status**: current status of credit card at month specified in "**card_status_months_ago**"
Legend for "**card_status**":
- 0: 1-29 days past due
- 1: 30-59 days past due
- 2: 60-89 days overdue
- 3: 90-119 days overdue
- 4: 120-149 days overdue
- 5: Overdue or bad debts, write-offs for more than 150 days
- C: paid off that month
- X: No loan for the month

## Feature Engineered Columns
- AMT_CARD_STATUS_ENTRIES: The length cardholder has been a customer
- MODE_CARD_STATUS: The most common card status present during cardholder status
- PCT_PAYMENTS_MISSED_GTR_AVG: Is the percent of missed payments greater than the median? Boolean value

## Cleaning the Data

- Renamed columns 
- Dropped occupation (majority data missing)
- Converted data to the proper types
- Label encoded the objects
- Used clients who have been a client for 6 months or longer

## Columns Used Building the Models
We used `feature importance` to find what columns had the biggest effect on our model. These columns were the most impactful:
- salary
- property_type
- age_days
- days_employed
- has_email
- AMT_CARD_STATUS_ENTRIES
- MODE_CARD_STATUS
- PCT_PAYMENTS_MISSED_GTR_AVG


## Percent Payment Model 
- Gradient Boosting Regressor
- Used GridSearchCV for hyperparameter tuning
- 84.5% Accuracy

## Mode Card Status Model 
- Gradient Boosting Classifier
- Used GridSearchCV for hyperparameter tuning
- 88% accuracy

### Analyzing Model Limitations
- Our model had a hard time predicting values between 30-70 for percent missing
- Data may not be able to tell us the values we were looking for, the featured engineered columns
- Data is unbalanced for classification but we are able to get clear predictions. There is an absence of data from the card status 1-5

# Findings & Suggestions 
- Majority of card holders miss all or none of their payments
- Salary, Property Type, Age, Days Employed, Has E-mail, Length of Card Holding, and Mode Card Status are important when analyzing cardholders
