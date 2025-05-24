# Exploratory Data Analysis (EDA): California Housing Prices

This repository contains an Exploratory Data Analysis (EDA) of the California Housing Prices dataset. The goal of this project is to thoroughly understand the dataset's characteristics, uncover key insights, identify potential data quality issues, and prepare the data for future machine learning modeling tasks.

## Table of Contents
- [Dataset Overview](#dataset-overview)
- [EDA Process and Methodology](#eda-process-and-methodology)
  - [Data Loading and Initial Inspection](#data-loading-and-initial-inspection)
  - [Data Cleaning](#data-cleaning)
  - [Univariate Analysis (Single Variable)](#univariate-analysis-single-variable)
  - [Bivariate Analysis (Relationships)](#bivariate-analysis-relationships)
  - [Feature Engineering](#feature-engineering)
  - [Correlation Analysis](#correlation-analysis)
- [Key Insights and Summary](#key-insights-and-summary)
- [Conclusion and Next Steps](#conclusion-and-next-steps)
- [Project Files](#project-files)

## Dataset Overview

The California Housing Prices dataset contains aggregated demographic and housing statistics for various districts in California, derived from the 1990 census. Each row represents a housing district.

**Key Features include:**
- `longitude`: A measure of how far west a house is.
- `latitude`: A measure of how far north a house is.
- `housing_median_age`: Median age of a house within a block.
- `total_rooms`: Total number of rooms within a block.
- `total_bedrooms`: Total number of bedrooms within a block.
- `population`: Total population within a block.
- `households`: Total number of households within a block.
- `median_income`: Median income for households within a block (in tens of thousands of US Dollars).
- `ocean_proximity`: Location of the house with respect to the ocean (categorical).
- `median_house_value`: Median house value for households within a block (in hundreds of thousands of US Dollars) - **This is our target variable.**

## EDA Process and Methodology

This EDA followed a systematic approach to explore the dataset comprehensively.

### Data Loading and Initial Inspection
The dataset was loaded using Pandas. Initial checks using `df.head()`, `df.info()`, and `df.describe()` were performed to understand the data types, non-null counts, and basic statistical summaries of each column.

### Data Cleaning
* **Missing Values in `total_bedrooms`**: Identified 207 missing values in the `total_bedrooms` column. These missing values were **imputed with the median value** of the column to preserve data integrity and ensure all rows could be used for analysis.

### Univariate Analysis (Single Variable)
* Histograms were generated for all numerical features to visualize their distributions. This revealed insights such as `median_income` having a long tail and `median_house_value` showing a peak at its maximum.
* A bar plot was used to visualize the distribution of the `ocean_proximity` categorical variable. This clearly showed that categories like `<1H OCEAN` and `INLAND` were the most prevalent, while `ISLAND` was extremely rare.

### Bivariate Analysis (Relationships)
* **`median_house_value` vs. `median_income` (Scatter Plot)**: An initial scatter plot demonstrated a strong positive linear relationship between `median_income` and `median_house_value`, indicating that higher median incomes generally correspond to higher median house values.
* **Data Capping Discovery**: A critical observation from the scatter plot was the **data capping** of `median_house_value` at **$500,001**. This means that any median house value exceeding this threshold was recorded as $500,001. This affected 965 rows, representing **4.68%** of the dataset. This is a crucial limitation to acknowledge for any predictive modeling.
* **`median_house_value` vs. `ocean_proximity` (Box Plot)**: Box plots were used to compare the distribution of `median_house_value` across different `ocean_proximity` categories. This analysis clearly showed that `ISLAND` properties have significantly higher median values, while `INLAND` properties are generally the least expensive. The influence of the $500,001 cap was also visible on the upper whiskers of several categories, notably `ISLAND`.

### Feature Engineering
To potentially enhance the predictive power of our features, three new features were engineered from existing numerical columns:
* `rooms_per_household` = `total_rooms` / `households`
* `bedrooms_per_room` = `total_bedrooms` / `total_rooms`
* `population_per_household` = `population` / `households`

### Correlation Analysis
A correlation matrix and its heatmap visualization were generated to understand the linear relationships between all numerical features, including the newly engineered ones.

## Key Insights and Summary

Based on the comprehensive EDA, the following key insights were drawn:

* The **`median_income`** is the most influential factor strongly and positively correlated with `median_house_value` (correlation: 0.69). This aligns with the expectation that higher income generally leads to higher housing investment.
* A significant data quality issue is the **capping of `median_house_value` at $500,001**, affecting 4.68% of the dataset. This means the dataset does not capture the true maximum values for high-end properties.
* Feature engineering revealed a **strong negative correlation** (-0.62) between `median_income` and `bedrooms_per_room`. This counter-intuitive relationship suggests that in higher-income areas, houses tend to have a lower ratio of bedrooms to total rooms, implying more spacious homes with dedicated non-bedroom areas (e.g., offices, dens).
* The `ocean_proximity` feature significantly impacts `median_house_value`, with `ISLAND` properties being the most expensive and `INLAND` properties being the least expensive.
* The relationship between `bedrooms_per_room` and `median_income` was the most surprising insight discovered, highlighting the nuanced composition of housing units across different income brackets.

## Conclusion and Next Steps

This EDA has provided a robust understanding of the California Housing Prices dataset, identifying crucial relationships, data quality issues, and potential areas for feature improvement. The insights gained are invaluable for the subsequent stages of a machine learning project.

The next steps for building a predictive model would include:
* Further data preprocessing, such as handling the `ocean_proximity` categorical feature (e.g., through one-hot encoding).
* Feature scaling for numerical features.
* Splitting the data into training and testing sets.
* Selecting, training, and evaluating various machine learning models to predict `median_house_value`.

## Project Files
- `California_Housing_EDA.ipynb`: The Jupyter notebook containing all the code, analysis, and visualizations for this EDA.
