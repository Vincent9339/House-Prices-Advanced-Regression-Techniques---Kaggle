# House Prices Advanced Regression Techniques [Kaggle] UNDER PROGRESS

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
- [Exploratory Data Analysis](#Exploratory-Data-Analysis): 
  - Understanding the Data Structure
  - [Target Variable Analysis (`SalePrice`)](#Target-Variable-Analysis)
  - [Univariate Analysis](#Univariate-Analysis)
  - [Bivariate Analysis](#Bivariate-Analysis)
  - [Correlation Analysis](#Correlation-Analysis)
  - [Data Cleaning](#Data-Cleaning)
- [Feature Engineering](#Feature-Engineering): 
- [Multicollinearity Check](#Multicollinearity-Check)
- [Time-Related Analysis](#Time-Related-Analysis)
- [Geographical Analysis](#Geographical-Analysis)
- [Model Training](#Model-Training):
- [Model Evaluation](#Model-Evaluation): 
## Explanation

### Target Variable Analysis

The graph shows that the tail on the right side of the distribution is longer than the left side. It means most house prices are concentrated on the lower end of the scale, with a few higher-priced homes pulling the average up. 

A positive skewness of **1.833** indicates that the majority of data points are clustered at the lower end of the scale, with a few extreme values extending the tail to the right, suggesting potential outliers or a need for data transformation.

### Missing values

I tackled missing values by: 

- **Finding Gaps**: Checked which columns had missing data and their percentages.  
- **Filling Blanks**: Used the mode for categorical features and the median for numerical ones. 
- **Final Cleanup**: Dropped any remaining rows with missing values.

### Outliers

#### Z-score Method:

#### How It Works:

The Z-score measures how many standard deviations a data point is from the mean of the distribution.
A common threshold for identifying outliers is to consider points as outliers if their Z-score is greater than 3 or less than -3.
This means that a point is considered an outlier if it is more than 3 standard deviations away from the mean.

- Result Interpretation:

The Z-score method is more sensitive to the overall shape of the data distribution. It assumes that the data follows a normal distribution (bell curve).
In practice, if the data is skewed (like real estate data often is), the Z-score method may miss some outliers because it relies heavily on the standard deviation.
In your case, it identified 16 outliers. This means there are 16 points where the GrLivArea or SalePrice deviates significantly (more than 3 standard deviations) from the mean.

#### IQR Method:

#### How It Works:

The Interquartile Range (IQR) method measures the spread of the middle 50% of the data, defined as the range between the 25th percentile (Q1) and 75th percentile (Q3).
Outliers are defined as points lying below Q1 - 1.5 * IQR or above Q3 + 1.5 * IQR.
This method is less sensitive to the shape of the data distribution and can work well even if the data is not normally distributed.

- Result Interpretation:

The IQR method tends to capture more outliers because it doesn't assume a normal distribution, making it suitable for skewed distributions like housing prices and living areas.
It identified 31 outliers in your data. This means that more data points are far from the middle range of the distribution, based on the spread of the data between the 25th and 75th percentiles.

#### Why the Difference?

- Skewed Data:

Real estate data, especially features like GrLivArea and SalePrice, are often right-skewed because a small number of properties tend to have much larger areas and higher prices than most others.
The Z-score method might underreport outliers in skewed data because it assumes a more symmetric distribution.
The IQR method, which is more focused on the range of the middle data points, tends to capture more outliers in such cases, identifying those points that are far from the core distribution.

- Different Sensitivity Levels:

The Z-score method is more conservative, flagging only extreme outliers.
The IQR method, with its focus on the interquartile range, is more sensitive to moderate deviations, which can lead to a higher count of identified outliers.

#### Summary

The Z-score method found 16 outliers because it identifies only the most extreme deviations from the mean, assuming the data is normally distributed.
The IQR method found 31 outliers because it considers any data point significantly outside the middle 50% range as an outlier, making it more suitable for the skewed nature of real estate data.
Choosing the method depends on the characteristics of the data and the objectives of your analysis. For real estate data, where distributions are often skewed, the IQR method might provide a more accurate picture of outliers.



### Univariate Analysis

#### Numerical values

Boxplot Interpretation


- **Q1 (First Quartile)**: **129,975**
  - This value represents the 25th percentile of the dataset, meaning that 25% of the houses in your dataset sold for less than or equal to **$129,975**. This indicates that a significant portion of the housing prices is clustered below this threshold.
- **Median**: **163,000**
  - The median represents the 50th percentile of the data. Therefore, 50% of the houses sold for less than or equal to **$163,000**, while the other 50% sold for more. The median is a better measure of central tendency in skewed distributions as it is less affected by outliers. In this case, it shows that the typical house price is around **$163,000**.
- **Q3 (Third Quartile)**: **214,000**
  - The third quartile indicates that 75% of the houses sold for less than or equal to **$214,000**. This means that only 25% of houses sold for prices above this value. The range between Q1 and Q3, known as the **interquartile range (IQR)**, is Q3−Q1=214,000−129,975=84,025Q3 - Q1 = 214,000 - 129,975 = 84,025Q3−Q1=214,000−129,975=84,025. This indicates a spread of **$84,025** between the lower and upper quartiles, suggesting a moderate degree of variability in the middle 50% of house prices.
- **Max**: **755,000**
  - The maximum value indicates that the highest sale price recorded in the dataset is **$755,000**. This is significantly higher than the third quartile, which suggests that there are high-value outliers or a small number of extremely expensive houses that have raised the maximum price considerably.
  - 

#### General Observations

1. **Distribution Shape**:
   - Since the median (163,000) is closer to Q1 (129,975) than to Q3 (214,000), the distribution of the house prices appears to be right-skewed. This means there are some higher-value properties that are pulling the average price up, which is consistent with the much higher maximum value (755,000).
2. **Outliers**:
   - Given that the maximum price is much higher than Q3, there may be potential outliers in the dataset. Outliers can indicate special cases, such as luxury homes or unique properties that differ significantly from the majority of the data.
3. **Variability**:
   - The IQR of **$84,025** indicates that the middle 50% of home prices are quite spread out, suggesting that there is a significant variety of property values in this dataset.
4. **Potential Implications**:
   - For potential buyers or investors, understanding this spread can help set realistic expectations regarding home prices. It may also indicate opportunities for investment in lower-priced properties.
5. **Price Segmentation**:
   - The presence of a large gap between Q3 and the max suggests there might be distinct segments in the housing market, where more affordable homes are clustered around the lower quartiles, while luxury homes push the higher end of the market.

#### Categorical values

Categorical features helps us understand the distribution of different categories within a variable. For example, analyzing the "KitchenQual" variable, which represents the quality of kitchens in houses, gives us a clearer picture of how different kitchen quality ratings are distributed across the dataset.

- **TA (Typical/Average):** 735 houses have a kitchen rated as "Typical/Average" quality, making it the most common category. This suggests that the majority of homes in the dataset have standard kitchen conditions without exceptional upgrades or downgrades.

- **GD (Good):** 586 houses have kitchens rated as "Good" quality, indicating a significant portion of homes have kitchens that are better than average but not quite top-tier. This category is also popular, showing a market preference for upgraded kitchens.

- **EX (Excellent):** 100 houses feature "Excellent" kitchen quality, representing homes with high-end kitchens that likely have superior materials and finishes. This is a smaller subset, suggesting that luxury kitchens are less common in the dataset.

- **Fa (Fair):** Only 39 houses have "Fair" kitchen quality, meaning that these kitchens are likely in need of updates or improvements. This small number indicates that few homes have subpar kitchen conditions.

### Correlation Analysis
![alt text](https://github.com/Vincent9339/House-Prices-Advanced-Regression-Techniques---Kaggle/blob/main/img/cor_mat_heatmap.png?raw=true)

Let's start with some examples from the graph.

- **TotRmsAbvGrd**: This variable counts the total number of rooms above the ground level, excluding bathrooms.
- **GrLivArea**: This variable measures the total area of the living space above ground, which includes all rooms and spaces considered livable.

A high positive correlation (e.g., close to +1) means that as the value of one variable increases, the other variable tends to increase as well.
In this case, homes with more rooms above ground typically have a larger above-ground living area. Thus, you can expect homes that have a higher count of total rooms to also have a greater square footage of livable space.


- **1stFlrSF**: This variable represents the total area of the first floor of the house.
- **TotalBsmtSF**: This variable measures the total area of the basement, which can include finished, unfinished, and any additional spaces below ground level.

This suggests that as the area of the first floor increases, the total area of the basement also tends to increase.
This relationship may imply that larger homes (with more living space on the first floor) are likely to have larger basements. Builders often design homes such that the first-floor area and basement area scale with the overall size of the property.

#### But what do I catch out of the box from Correlation
![alt text](https://github.com/Vincent9339/House-Prices-Advanced-Regression-Techniques---Kaggle/blob/main/img/cor_vs_target.png?raw=true)
#### Positive Correlation

- High Correlation with GrLivArea:

A high positive correlation between SalePrice and GrLivArea indicates that as the above-ground living area of a property increases, the sale price also tends to increase. This suggests that buyers place significant value on the amount of livable space in a home; larger homes with more square footage generally command higher prices in the real estate market.
High Correlation with OverallQual:

The strong positive correlation between SalePrice and OverallQual signifies that properties with better material quality and overall finish tend to sell for higher prices. This reflects a market preference for well-constructed homes with higher-quality finishes, indicating that quality significantly impacts a buyer's willingness to pay.

#### Negative Correlation

- Negative Correlation with KitchenAbvGr:

The negative correlation between SalePrice and KitchenAbvGr suggests that an increase in the number of kitchens above ground is associated with lower sale prices. This may imply that homes with multiple kitchens are less desirable or may indicate a property designed for a different market segment, such as multi-family units, which might not attract the same pricing as single-family homes.
Negative Correlation with EnclosedPorch:

The negative correlation between SalePrice and EnclosedPorch indicates that an increase in the area of enclosed porches is associated with a decrease in sale price. This could suggest that, in this dataset, buyers might prefer open spaces or patios over enclosed porches, possibly due to preferences for outdoor living areas rather than enclosed additions, impacting the perceived value of the property.





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

