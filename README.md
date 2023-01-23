# BANK DIRECT MARKETING -  
# AN APPLICATION OF THE CRISP-DM METHODOLOGY

## Business Understanding
A bank in Portugal used its call center to do direct 17 direct marketing campaigns between May 2008 and November 2010 for 41,118 prospects.
This project has two objectives:
- Develop a model to identify the prospects who are more likely to respond to the offer by the bank
- Uncover the exegenous factors which make them more favorable candidates during a marketing campaign

## Data Understanding
Several steps were taken to get to know the dataset and identify any data quality issues with the dataset.
- Review of the columns in the dataset:
  - Do we have a good understanding of all the columns in the dataset?
  - Which columns can be used for the prediction problem?
  - Are there any columns not required for the modeling problem?
  - Is the relationship between the input variables and target explainable and palatable?
  - Is there any collinearity in the development sample?
 
- Review of the rows in the dataset:
  - Are there sufficient records for the prediction problem?
  - Are there any duplicate records?
  - Are there any outliers?
  - Are there any records with missing values that can be excluded from the analysis sample?
  - How do you deal with records with "unknown" values for the columns we want to keep for modeling?

## Data Preparation
Any issues with the data were resolved in this step:
- Removed the duplicate records from the analysis sample.
- Dropped the 'duration' variable since it is a target leaker. The duration is not known before the call is made, and therefore cannot be used for model implementation.
- Dropped variables highly correlated with the other variables.
- Hot encoded and label encoded the categorical variables.
- Tested interaction variables (2-degree polynomial)
- Prepared train (75%) and test (25%) samples for model development.

## Modeling
We developed kNN, logistic regression, decision tree and SVM models:
| Model     | Hyperparameters | Variable Set |Additional Treatment| AUC_Test|
| :---        |    :----   |   :---|   :---|  :---|
|kNN|Default|Customer|None|0.587|
|Logistic Regression|Default|Customer|None|0.647|
|Decision Tree|Default|Customer|None|0.618|
|SVM|Default|Customer |None|0.538|
|kNN|Default|Customer + Contact + Contextual|None|0.741|
|Logistic Regression|Default|Customer + Contact + Contextual|None|0.802|
|Decision Tree|Default|Customer + Contact + Contextual|None|0.621|
|Logistic Regression|Default|Customer + Contact + Contextual|Drop variables with very low coefficient values|0.803|
|Logistic Regression|Default|Customer + Contact + Contextual|Drop variables with very low coefficient values, Polynomial transformation to detect interaction|0.805|
|Logistic Regression|Variable Section of 20 variables, Penalty = L2, C = 100|Customer + Contact + Contextual|Drop variables with very low coefficient values|0.803|

##Evaluation

Logistic regression performed better than the other models in terms of the higher performance metrics and shorter runtimes. Even though we improved the AUC from 0.647 to 0.805, more research is required to further enhance the model's predictive power.

The following customers are more likely to accept the offer compared with the other segments of the population:
- Did not default on their prior credit obligations.
- Students and retired
- Older prospects
- Single
- Customers who are admin and work at services

The economic environment is also a factor in the customer behavior. During an economic downturn, prospects have less appetite to open a term deposit account.

# Deployment

Our recommendations for next steps are summarized as follows:
- The model may benefit from further research on the variable selection criteria. A more thorough analysis should be done to eliminate the non-palatable and autocorrelated variables from the dataset.

- The bank may be contacted and asked if we could get the campaign date for each record dataset. This level of detail will help us better understand if some marketing campaigns have yielded more favorable subscription rates. Data for Some campaigns that are not relevant anymore may be excluded from model development.

- A cost-benefit analysis (cost of contacting a customer vs. profit of a booked account) may be done to associate the performance metrics with the $ values.

You can find the Jupyter notebook in this location: https://github.com/SunaHafizogullari/SunaHafizogullari-BerkeleyMLCertificate-BankMarketingCampaign/blob/main/prompt_III_SunaHafizogullari.ipynb
