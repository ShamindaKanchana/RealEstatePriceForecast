# Real Estate Price Forecast

This project utilizes the Bangalore House Price dataset to predict house prices using machine learning models. The aim is to build a robust model that helps in estimating property prices based on features like location, total square footage, number of bathrooms, and more.

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset Information](#dataset-information)
- [Data Preparation](#data-preparation)
- [Data Preprocessing](#data-preprocessing)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Feature Engineering](#feature-engineering)
- [Model Building](#model-building)
- [Model Evaluation](#model-evaluation)
- [Conclusion](#conclusion)
- [Future Work](#future-work)
- [How to Run the Project](#how-to-run-the-project)

## Project Overview
The goal of this project is to predict house prices based on various features such as area type, location, size, number of bathrooms, and total square footage. The project leverages machine learning models to predict the target variable, `price`.

## Dataset Information
- **Source**: [Kaggle Bangalore House Price Data](https://www.kaggle.com/amitabhajoy/bengaluru-house-price-data)
- **Key Columns**:
  - `area_type`: Type of area (built-up, super built-up, etc.)
  - `availability`: Property availability status (immediate possession, ready-to-move)
  - `location`: Location of the property
  - `size`: Number of bedrooms
  - `society`: Housing society (if applicable)
  - `total_sqft`: Total area in square feet
  - `bath`: Number of bathrooms
  - `balcony`: Number of balconies
  - `price`: Price of the property (target variable)


## Data Preparation
After reviewing the features, it was determined that the columns `area_type`, `society`, `balcony`, and `availability` do not significantly contribute to house price prediction. Therefore, these columns were dropped to streamline the analysis.



## Data PreProcessing

### Handling Null Values
- Checked for null values in the dataset.
- Rows with null values were removed to ensure a clean dataset for analysis.

### Size column Standardlization
The size column contained various representations for the number of bedrooms, such as "4 Bedroom" and "4 BHK". To standardize this, the following steps were taken:
- Extracted the numerical part of each entry using regular expressions
- Created a new column `BHK` with these numerical values for consistency.

### Location Data Reduction
The location column had many unique values. To manage the dimensionality for one-hot encoding, locations with fewer than 10 occurrences were grouped under a common label 'others'. This resulted in reducing the number of unique locations to 242.

### Outlier Treatment

#### 1. Bedroom Size Outliers
In this project, we identified that a typical bedroom should have at least 300 square feet of space. Any data points where the total square footage per bedroom (`total_sqft_con` / `BHK`) was less than 300 were considered outliers. These outliers were removed to ensure that the data only contains realistic property configurations, which improves the accuracy of our house price predictions.

#### 2. Price Per Square Foot (PPS) Outliers
Additionally, we assumed that in the same location, properties with prices per square foot (PPS) that deviate beyond the first standard deviation from the mean are outliers. These properties were removed to ensure that the dataset only includes properties with typical pricing trends for their respective locations.

This approach prevents extreme values from skewing the prediction model by focusing on properties with reasonable price variations within each location.


