# credit-card-churn-predict-eda

**Balvinder Sabharwal**

#### Executive summary

#### Rationale
Why should anyone care about this question?

At the heart of any business model is the relationship between the business and their customers. Customers are the most important asset of the business and is the sole reason for the business to exist. It is very important for business to maintain good relationship with customers and proactively work to understand the expectations, needs and complaints of the customers to retain the customers. Customer churn prediction is the problem which is relevant across different industries, retaining the customers is important for every industry whether it is credit card company, telecom company, banking, retail or any other industry. The companies must have strong capabilities to predict which customers can leave so they can take proactive measures like target marketing, discounts or other measures to retain them.

#### Research Question
What are you trying to answer?

Predicting the customer who are more likely to leave the credit card services so that the credit card company can proactively reach out to them with better services and products and make them stay with the company.

#### Data Sources
What data will you use to answer you question?

Dataset is of Credit Cards customer data. This dataset includes the following data
- Product data like card category
- Customer Demographic data like age, gender, income level, dependents, education level, marital status
- Customer engagement data like total relationship count, months on book, months inactive, contacts count, average card utilization ratio
- Customer spending data like credit limit, total transaction count, total transaction amount, revolving balance
- Customer attrition indicator
Source - https://www.kaggle.com/datasets/sakshigoyal7/credit-card-customers/data

#### Methodology
What methods are you using to answer the question?

- Baseline - LogisticRegression
- Classification Algorithms - KNN, Decision Trees, SVM
- Ensemble techniques - Random Forest, XGBoost
- Neural Networks

#### Results
What did your research find?

EDA Observations
- The dataset is imbalanced between the two classes 'Existing Customer and 'Attrited customer' with 84% as existing customer and 16% as attrited customer
- There are big outliers seen on higher side for the Credit limit which is casing the mean to be almost double of median and making the data for this column right skewed.
- Right skewness also seen for Avg_Open_To_Buy and Total_Trans_Amt columns.
- There is no null values in the dataset but for categorical columns Income_category, Education_Level and Marital Status the missing values are put in their own category as 'Unknown'.
- The scatter plot for relationship between Total_Trans_Ct and Total_Trans_Amt shows the concentration of Attrited customers towards lower transactions count and amount.
-The scatter plot between Months on book and Total Trans Amount shows that customers who are spending upward of 12k on the card are happy with the services and are not likely to churn Also at the 36 months we see the maximum concentration of Attrited customers.
- The boxplot for Contacts Count in 12 months shows higher median value for Attrited customers compared to Existing customers.
- The KDE plot clearly shows that for the majority of Attrited Customers the Avg Utilization ratio drops to zero before they leave the service.
- There seems to be partial relationship between income category and credit limit with clear correlation on the lower side of the income category unto 60k. But 60k+ shows no direct correlation. 

Feature Engineering

As part of feature engineering, two new columns are created
- Avg_Transaction_Size - This column is calculated by dividing the Total_Trans_Amt with Total_Trans_Ct to create the column to get insight into the average spending of the customer per transaction
- Unused_Credit_Buffer - This column is calculated by subtracting the Total_Revolving_Bal from Credit_Limit to create the column to get insight into the credit usage of the customer.

The following column transformations are applied to the columns
- The columns with data type object has been changed to Category except for the target variable Attrition_Flag since pandas internally creates a reference map for these categories with integer to string mapping and then store the memory efficient integers instead of strings for all the rows providing huge memory optimizations.
- Numerical columns are transformed using StandardScaler
- Categorical columns except Education Level are transformed using OnHotEncoder
- Education_Level column is transformed using OrdinalEncoder with the custom defined order of the education levels.
- The target variable Attrition_Flag is mapped as Existing Customers as 0 and Attrited Customer as 1

Baseline Model

We used LogisticRegression as the model to baseline results. Interpreting the results of the Logistic Regression model with only setting the class_weigth='balalnced' and no other hyperparameter configuration we observe the following results
- The training accuracy (86.2%) and test accuracy of (85.7%) are very close which indicates that Logistic Regression model is generalizing on the unseen data and there is no overfitting
- Since the dataset is highly imbalanced with the majority class as 84% and minority class as 16%, a completely random model which simply guesses majority class every time will still have accuracy score of 84%. Our Logistic Regression model has accuracy of 86% it is performing better than the dummy model. However we need to look at other metrics like Recall and Precision to get deeper insight into the model performance.
- For the majority class Existing Customers(0), of all the instances that model labelled as 0, we see the Precision score of 97% which indicates very high accuracy of correctly predicting the majority class. The Recall score for majority class is 86% which means it was able to find 86% of all the actual majority class (Existing Customer) instances
- For the minority class Attrited Customer(1) which has a more critical focus since our problem is to predict the attrition, the Recall score is 86% which is phenomenal result since we are able to find 86% of the instances of the minority class(1) in an highly imbalanced dataset. However looking at the Precision score for the minority class(1) we see it as 54% which means of all the instances it flagging as attrition only 54% are actually true creating large False Positives. This can be problematic since it is generating lot of false alarms and we need to find ways to increase the Precision for the minority class.
- As part of baselining the results, Logistic Regression and Ridge Classifier with GridSearchCV was also tried to find the best parameters for the regularization. The results for both Logistic Regression and Ridge Classifier using GridSearch CV were almost identical to Logistic Regression. Please refer to the Jupiter notebook for more details.



#### Next steps
What suggestions do you have for next steps?

#### Outline of project

- [[Link to notebook 1]()](https://github.com/bssabharwal/credit-card-churn-predict-eda/blob/main/notebook/credit_card_churn_predict_eda.ipynb)
- [Link to notebook 2]()
- [Link to notebook 3]()


##### Contact and Further Information
