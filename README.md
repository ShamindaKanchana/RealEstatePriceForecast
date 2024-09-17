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


### 3.Outlier Treatment: Bathroom to Bedroom Ratio
In real estate data, it is typically expected that the number of bathrooms should not significantly exceed the number of bedrooms. For example, a house with two bedrooms and four bathrooms is highly unlikely and represents an outlier in the dataset.

- Criteria: Properties with an unusually high number of bathrooms compared to bedrooms were identified as outliers.
- Action: We removed these outliers to ensure the dataset remains realistic and reliable. Since the number of such instances was minimal, their removal did not affect the overall distribution of the data.

### 4.Outlier Treatment: BHK-Based Price Filtering
In our dataset, we observed that certain properties had anomalously low prices per square foot (pps) when compared to similar properties with fewer bedrooms in the same location. These were considered outliers since larger properties are generally expected to have similar or higher prices per square foot.



- Criteria: For each location, properties with more bedrooms (BHK) were compared to those with fewer bedrooms. If the price per square foot of a property with more bedrooms was significantly lower than the average price per square foot of properties with fewer bedrooms (within the same location), it was identified as an outlier.

- Action:Outliers were removed if the price per square foot was lower than the average price for properties with fewer bedrooms in the same location. To ensure statistical significance, this was only applied to locations where there were more than five properties in a particular bedroom category.