# House Prices Advanced Regression Techniques [Kaggle]

## Overview
This project aims to predict house prices from a Kaggle competition, based on various features of the houses. The dataset contains information about various attributes of houses sold, which will be analyzed and used to create a predictive model for house prices.

## Dataset
The dataset used in this project is sourced from the [Kaggle House Prices: Advanced Regression Techniques competition](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data). It includes the following key columns:

- **SalePrice**: The property's sale price in dollars (target variable).
- **MSZoning**: General zoning classification.
- **LotFrontage**: Linear feet of street connected to the property.
- **LotArea**: Lot size in square feet.
- **OverallQual**: Overall material and finish quality.
- **GrLivArea**: Above grade (ground) living area square feet.
- **...** *(additional relevant columns)*

## Objective
The primary objective is to create a model that accurately predicts the sale price of houses based on the various features available in the dataset. This project involves exploratory data analysis, feature engineering, model selection, and evaluation.

## Steps Involved
- [Exploratory Data Analysis](#Exploratory Data Analysis): Analyzing the dataset for patterns, trends, and relationships.
  - Understanding the Data Structure
  - Target Variable Analysis (`SalePrice`)
  - Univariate Analysis
    - Numerical Features
    - Categorical Features
  - Bivariate Analysis
    - Numerical Features vs. SalePrice
    - Categorical Features vs. SalePrice
  - Correlation Analysis
  - Data Cleaning
    - [Missing values](# Data Cleaning[Missing values])
    - [Outliers](# Data Cleaning[Outliers])
- **Feature Engineering**: Creating new features or modifying existing ones to improve model performance.
  - Potential Derived Features
  - Log Transformation
- **Multicollinearity Check**
  - Variance Inflation Factor
- **Time-Related Analysis**
- **Geographical Analysis**
- **Model Training**: Using various regression models to predict house prices.
- **Model Evaluation**: Assessing model performance using metrics such as Mean Absolute Error (MAE), Mean Squared Error (MSE), and R-squared (R²).

## Explanation

### Exploratory Data Analysis

### Data Cleaning[Missing values]

I tackled missing values by: 

- **Finding Gaps**: Checked which columns had missing data and their percentages.  
- **Filling Blanks**: Used the mode for categorical features and the median for numerical ones. 
- **Final Cleanup**: Dropped any remaining rows with missing values.

### Data Cleaning[Outliers]

## Usage

You can explore this notebook to understand the methods and analyses conducted. The results of various models and their evaluations will help you understand the factors influencing house prices.

## Results

The project includes visualizations and model performance metrics. Key findings from the analysis include:

- **Feature Importance**: Identifying which features are most predictive of sale price.
- **Model Performance**: Comparison of different models based on their evaluation metrics.

## Conclusion

This project demonstrates how to apply data science techniques to predict house prices effectively. The insights gained can be beneficial for real estate professionals and potential homebuyers.

## License

This project is licensed under the MIT License. See the LICENSE file for more details.

## Acknowledgments

- Special thanks to Kaggle for providing the dataset and the platform for sharing data science projects.
- References to any relevant literature or tutorials that assisted in the completion of this project.

