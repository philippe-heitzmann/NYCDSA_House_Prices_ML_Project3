### Project Overview 

The objective of this project was to build machine learning models to predict house prices as part of the Kaggle competition [House Prices: Advanced Regression Techniques](https://www.kaggle.com/c/house-prices-advanced-regression-techniques). The dataset used in this competition was the Ames Housing dataset, which was compiled by Professor Dean De Cock of Truman State University and which describes the sale of residential properties in Ames, Iowa during the period 2006 - 2010. The dataset contains a total of 2919 observations split across 80 different explanatory variables (23 nominal, 23 ordinal, 14 discrete, and 20 continuous) that impact home values, captured in the SalePrice variable in this dataset.


### Machine Learning Takeaways

Subsequent to Exploratory Data Analysis, Data Preprocessing, Feature Engineering and Feature Selection on our data, we apply **Ridge, Lasso, Random Forests Regressor, Gradient Boosting Regressor and XGBoost** machine learning models to this dataset in order to test the strengths and weaknesses of each model on this dataset. Careful hyperparameter tuning of each model produced the following cross-validated negative Root Mean Squared Error scores and Kaggle Scores (lower is better) for each of our models:

| Model             | Variables Used | CV Neg RMSE | Kaggle Score |   
|-------------------|----------------|-------------|--------------|
| Ridge             | 99             | -766k       | 0.1458       |   
| Lasso             | 98             | -780k       | 0.1403       |   
| Gradient Boosting | All variables  | -548k       | 0.1367       |   
| Random Forest     | All variables  | -714k       | 0.1395       |   
| XGBoost           | 151            | -687k       | 0.1388       |   
                                                         

We proceed to stack these 'Level 0' models in to a 'Level 1' model trained on top of the house price predictions outputted by our Ridge, Lasso, RandomForests, XGBoost, and Gradient Boosting Models. This stacked 'meta-model' outperformed all individual model components and yielded a final Kaggle score of **0.13072**.


### Model Feature Importance Insights & Conclusion

Given our stacked Level 1 model trains on the predictions of the Level 0 models, I wanted to take a step back to analyze the feature importances in our Level 0 models. The following are some of the insights gleaned from the outputted feature importances of each model as well as some recommendations for residential real estate buyers and sellers:

1. **XGBoost**: Qualitative variables such as OverallQual and ExterQual are most important

    *Sellers*: Consider investing more into quality of the external finish of a house to fetch higher prices
    
    *Buyers*: Consider buying houses with no/low-quality basements and excavating/enlarging/improving these yourself if cheaper in the aggregate

1. **Random Forests**: OverallQual, TotalArea, Area1stArea2nd, LotFrontage are most important

    *Sellers*: Consider improving fireplace quality to fetch higher prices
    
    *Buyers*: Consider buying houses with no garage and building one yourself if cheaper in the aggregate

1. **Gradient Boosting Regressor**: OverallQual, LotArea, BsmtQual & YearBuilt are most important

    *Sellers*: Consider investing in Central Air conditioning to fetch higher prices
    
    *Buyers*: Consider buying older houses and remodeling these yourself

1. **Linear Models**: LotArea, Neighborhood variables are most important

    *Sellers*: Consider building an open porch to increase house value
    
    *Buyers*: Consider building an open porch yourself to save money if cheaper in the aggregate
