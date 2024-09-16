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

## Handling Null Values
- Checked for null values in the dataset.
- Rows with null values were removed to ensure a clean dataset for analysis.

### Size column Standardlization
The size column contained various representations for the number of bedrooms, such as "4 Bedroom" and "4 BHK". To standardize this, the following steps were taken:
- Extracted the numerical part of each entry using regular expressions
- Created a new column `BHK` with these numerical values for consistency.