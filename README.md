# Loan Default Data Predictions
In the loaning industry, it is important to identify if loans that are funded will be paid back and not defaulted on. In many cases, this is the most important question. This project aims to ascertain which factors increase customers' likelihood of failing to pay loans back and then, based on the results of the project, make reccomendations to decrease the share of loans that are failed to pay back.
The data sourced for this project is anonymous data from Kaggle.com (https://www.kaggle.com/datasets/joebeachcapital/loan-default?select=Anonymize_Loan_Default_data.csv)
## Methodology 
For this project, I used excel. The dataset provides a binary classification of customer's loans as the column "repay_fail" and using this I ran a logistic regression. To do this, I first selected variables that in my experience hold significance in predicting customer success. This includes the following categories from the dataset: "funded_amnt" "annual_inc" "dti" "addr_state" which identify customers' amount of funds extended to them, how much money they make in a year, their debt-to-income ratio, and the state they are from respectively. To complete this logistic regression, I used the add-in "Real Statistics Resource Pack" (https://real-statistics.com/free-download/real-statistics-resource-pack/). After obtaining the results of logistic regression, I used the coefficients to calculate the Odds Ratios (OR) of each variable. After this, I determined which Odds Ratios were statistically significant and examined the effects of these. 
### Considerations
  **DATA CLEANING**
    This dataset required minimal data cleaning. A few rows were omitted due to "NA" values in either all categories or in multiple meaningful categories. 
    
  **FILTERING**
    In the dataset, I determined that the system from the anonymous loan data starts all customers off as "0" in the "repay_fail" column, that changes to a "1" indicating failure to pay. However, this change happens when customers extend past their grace period. For the purposes of this project, only customers who are in "true default" (a state in which a customer is fully charged off, with no repayment plans present, after all grace periods) need to be considered. To acheive this, I filtered for customers who had a "1" in their "repay_fail" column, but who also had NA in their "next_pymnt_d(next payment date)" column. This generates a list of customers who have extended past their grace period, and have no payments scheduled (this means the failure of their repayment is more accurately solidified).

**TRANSFORMATIONS**
  This project incorporates a few transformations of the data. One transformation involved dividing all incomes under the "annual_inc" by a factor of 1000 (this transformation was necessary to allow computations in excel while avoiding #NUM! errors; /1000 to be kept in mind if using coefficients to make predictions). Another is centered around the variable "addr_state." Since a customer's state is a categorical variable, I had to convert each customer's state binarily using dummy variables. To do this, I used California as the comparison group (California constitutes the majority of loans in the dataset, with the highest variance in all categories chosen and thusly is a good "control" group for the binary classification). 

  **ASSUMPTIONS**
    Though not explained in the source of the dataset, I operated with a few assumptions in mind. The state of North Dakota is omitted from the source data. The assumption would be that the loan company might be based out of North Dakota and does not lend within the state (especially if the company is a part of a tribal lending operation). Another assumption is that the dataset is a snapshot of a loaning data for an unspecified length of time as opposed to the complete loan portfolio of the company.
## Findings
  The results show that biggest predictor of whether a customer would truly default on their loan is if they are in the state of Nevada. The numbers show that people from Nevada are roughly 20% more likely to default than the control group, while some states actually decreased the liklihood (though the states with the most pronounced effect have not had a sufficient sample size to rule out sampling error). A customer's annual income, dti, and funded amount had no statistically significant effect on customer's failure to pay.
## Recommendations
  Based on the results I found, it is recommended for a period of time to not loan in the state of Nevada. This would not be definite, and would only be for a period of time that allows an adequate amount of new loans to be processed. 



