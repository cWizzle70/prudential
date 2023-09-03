## Objective
Explore the Prudential Life Insurance dataset providing insights, split the data into train and test datasets, and perform a comparison of the performance of models in categorizing applicants under Response.

## Steps
- Explore the dataset
- Share insights into the relationships between features
- Split the data into training and test datasets
- Clean the data by handling any missing or NaN values
- Optimize the data for training
- Train the models
- Analyse the results

## Data Exploration
- The dataset consists of 128 features and 59381 entries.
- The data can be grouped into sub-categories:
    - Bio
        - Ht
        - Wt
        - BMI
        - Ins_Age
    - Product_Info
    - Employment_Info
    - InsuredInfo
    - Insurance_History
    - Family_History
    - Medical_History
    - Medical_Keyword
    - Response (Target Variable)
- The plot 'Frequency of Response Category' shows the majority of applicants categorised as an 8 while the minority are categorised as 3 and 4
- There are 3 data types in the dataset:
    - int (109 features)
    - float (18 features)
    - object (1 features)

## Insights
- The plot 'Most highly correlated columns' shows the correlations between the 20 features with the highest mean correlation
- It highlights Medical_History_23 and Medical_History_15 as having the highest correlation with Response with correlation values of 0.29 and 0.29, respectively
- The plot also highlights other strong correlatons like Medical_History_24 and Medical_History_10 with a correlation of 0.81
- The plot 'Columns correlated with Response' shows the features with the highest correlation with Response and their respective correlation values, Medical_History_23 and BMI having the highest correlations
- Figures 1-4 show Kernel Density Estimation (KDE) plots for 4 sub-categories: Bio, Family_History, Product_Info and Insurance_History
- These KDE plots show the probability per Response category given a value assigned to the corresponding feature

## Data Quality and Optimization
- The data has a high number of missing values with Medical_History_10 missing 99.06% of its values
- This was addressed after splitting the data into train and test datasets with a train:test ratio of 80:20
- The split was stratified to ensure an even distribution of Response categories across each set
- This distribution is shown in the plot 'Distribution of Response values across Original, Training and Test data'
- Features with more tha 40% missing values were removed from the dataset with the remaining missing values estimated using Iterative Imputation
- Product_Info_2 contained nominal values and was encoded with One Hot Encoding
- The data was normalised to minimize any biases
- Multicollinearity was identified using Variance Inflation Factor (VIF) which showed a large number of features with high VIF scores
- Least Absolute Shrinkage and Selection Operator (LASSO) feature selection was used to remove features with a variance coefficient of 0, leaving only features of interest in the dataset

## Models
- Four types of models were trained and tested
    - Logistic regression model: LogisticRegression (sklearn)
    - Decision Tree: RandomForestClassifier (sklearn)
    - Gradient Boosting: GradientBoostingClassifier (sklearn)
    - Extreme Gradient Boosting: XGBClassifier (xgboost)
- Training durations:
    - LogisticRegression: 26 seconds
    - RandomForestClassifier: 15 seconds
    - GradientBoostingClassifier: 4 minutes 46 seconds
    - XGBClassifier: 2 minutes 27 seconds

## Performance

| Model                      | Accuracy  | Precision | Recall   |
|----------------------------|-----------|-----------|----------|
| LogisticRegression         | 0.483371  | 0.443826  | 0.483371 |
| RandomForestClassifier     | 0.531279  | 0.500435  | 0.531279 |
| GradientBoostingClassifier | 0.540709  | 0.517150  | 0.540709 |
| XGBClassifier              | 0.545256  | 0.518939  | 0.545256 |

- The four models had similar performance with GradientBoostingClassifier and XGBClassifier being the better two
- The metrics are disappointing but could be improved by:
    - Increasing the amount of training data
    - Tuning the models by providing hyper parameters