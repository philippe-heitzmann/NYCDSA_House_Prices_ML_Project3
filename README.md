# House Prices Prediction - Ames, Iowa

A comprehensive machine learning project for predicting house prices using the Ames Housing dataset from the [Kaggle House Prices: Advanced Regression Techniques competition](https://www.kaggle.com/c/house-prices-advanced-regression-techniques).

## Project Overview

This project implements advanced machine learning techniques to predict residential property prices in Ames, Iowa. The dataset contains 2,919 observations with 80 explanatory variables describing various aspects of residential properties sold between 2006-2010.

### Dataset Details
- **Source**: Ames Housing dataset by Professor Dean De Cock (Truman State University)
- **Time Period**: 2006-2010
- **Observations**: 2,919 properties
- **Features**: 80 variables (23 nominal, 23 ordinal, 14 discrete, 20 continuous)
- **Target**: SalePrice (continuous variable)

## Project Objectives

- Build powerful predictive models for house price estimation
- Develop object-oriented programming skills through custom preprocessing and modeling classes
- Gain deeper understanding of different ML algorithms and their strengths/weaknesses
- Implement ensemble methods and model stacking for improved performance

## Results Summary

### Individual Model Performance

| Model             | Features Used | CV RMSE | Kaggle Score |
|-------------------|---------------|---------|--------------|
| Ridge             | 99            | 0.766k  | 0.1458       |
| Lasso             | 98            | 0.780k  | 0.1403       |
| Gradient Boosting | All features  | 0.548k  | 0.1367       |
| Random Forest     | All features  | 0.714k  | 0.1395       |
| XGBoost           | 151           | 0.687k  | 0.1388       |

### Final Performance
**Best Kaggle Score: 0.13072** (using stacked ensemble model)

## 🔧 Methodology

### 1. Data Preprocessing
- **Outlier Detection & Removal**: Identified and removed extreme outliers in GrLivArea and LotFrontage
- **Missing Value Imputation**: Strategic imputation based on data understanding
- **Feature Engineering**: Created 20+ new features including:
  - TotalArea (sum of all area-related features)
  - Age (YrSold - YearBuilt)
  - Binary indicators for various amenities
  - Ordinal encoding for quality variables

### 2. Feature Selection
- **Correlation Analysis**: Selected features based on correlation thresholds
- **Recursive Feature Elimination (RFE)**: Used RFECV for optimal feature selection per model
- **Model-Specific Selection**: Different feature sets optimized for each algorithm

### 3. Model Training & Tuning
- **Hyperparameter Optimization**: GridSearchCV with 3-fold cross-validation
- **Multiple Algorithms**: Ridge, Lasso, Random Forest, Gradient Boosting, XGBoost
- **Performance Metrics**: Root Mean Squared Error (RMSE) and R² score

### 4. Ensemble Methods
- **Model Stacking**: Level-0 models (base learners) + Level-1 meta-model
- **Meta-Learners**: Linear Regression, Gradient Boosting, XGBoost
- **Final Prediction**: Best performing stacked ensemble

## Key Insights

### Most Important Features Across Models

1. **XGBoost**: OverallQual, ExterQual (quality variables)
2. **Random Forest**: OverallQual, TotalArea, Area1st2nd, LotFrontage
3. **Gradient Boosting**: OverallQual, LotArea, BsmtQual, YearBuilt
4. **Linear Models**: LotArea, Neighborhood variables

### Business Recommendations

**For Sellers:**
- Invest in external finish quality (OverallQual, ExterQual)
- Consider adding central air conditioning
- Improve fireplace quality
- Build open porches for added value

**For Buyers:**
- Consider houses with lower basement quality for renovation potential
- Look for properties without garages for DIY construction
- Older houses offer remodeling opportunities
- Evaluate neighborhood carefully as it significantly impacts price

## 📁 Project Structure

```
├── README.md                           # Project documentation
├── Objectives.md                       # Project objectives and evaluation criteria
├── main_analysis.ipynb                 # Main analysis notebook (consolidated)
├── data/                              # Data directory (if applicable)
└── results/                           # Model outputs and predictions
```

## Getting Started

### Option 1: Local Python Environment

1. **Prerequisites**:
   - Python 3.7+
   - Required packages: pandas, numpy, scikit-learn, xgboost, matplotlib, seaborn

2. **Data Setup**:
   - Download the Ames Housing dataset from Kaggle
   - Place `train.csv` and `test.csv` in the project directory

3. **Running the Analysis**:
   - Open `main_analysis.ipynb`
   - Execute cells sequentially
   - Results will be saved as CSV files

### Option 2: Docker Environment

1. **Prerequisites**:
   - Docker installed on your system
   - Ames Housing dataset downloaded from Kaggle

2. **Data Setup**:
   - Place `train.csv` and `test.csv` in the project directory

3. **Build and Run Docker Container**:
   ```bash
   # Build the Docker image
   docker build -t house-prices-ml .
   
   # Run the container with Jupyter notebook
   docker run -p 8888:8888 -v $(pwd):/usr/src/app house-prices-ml
   ```

4. **Access Jupyter Notebook**:
   - Open your browser and go to `http://localhost:8888`
   - Use the token provided in the terminal output to access the notebook
   - Open `main_analysis.ipynb` and execute cells sequentially
   - Results will be saved as CSV files in the project directory

5. **Stop the Container**:
   - Press `Ctrl+C` in the terminal to stop the container
   - Or run `docker stop <container_id>` in another terminal

## Model Performance Details

The project achieved a **0.13072 Kaggle score** using a sophisticated stacking approach:

1. **Level-0 Models**: Individual tuned models (Ridge, Lasso, Random Forest, Gradient Boosting, XGBoost)
2. **Level-1 Meta-Model**: Gradient Boosting Regressor trained on Level-0 predictions
3. **Cross-Validation**: 3-fold CV for robust performance estimation
4. **Feature Selection**: RFECV-optimized feature sets for each model

## 🔗 Additional Resources

- [Full Blog Post](https://nycdatascience.com/blog/student-works/machine-learning-predicting-house-prices-in-ames-ia/)
- [Kaggle Competition](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)
- [Ames Housing Dataset Documentation](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data)

## License

This project is part of the NYC Data Science Academy curriculum and is for educational purposes.
