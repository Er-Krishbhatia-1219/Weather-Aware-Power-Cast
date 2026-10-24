# Weather-Aware Power Forecasting

## Overview

**Weather-Aware Power Forecasting** is a machine learning regression project designed to predict electricity demand using historical power-consumption records, weather conditions, and time-based variables.

The project combines **data analytics**, **feature engineering**, and **predictive regression modelling** to understand how electricity demand changes with temperature, humidity, rainfall, wind speed, time, day, month, and seasonal patterns.

The objective is to support **energy-demand planning**, **load forecasting**, **grid optimization**, and **data-driven operational decision-making**.

---

## Business Problem

Electricity demand varies continuously because of changing weather conditions, consumer usage patterns, peak hours, and seasonal effects. Inaccurate demand forecasting can lead to:

- Excess electricity generation and increased operational cost
- Insufficient supply during peak-demand periods
- Inefficient energy-resource allocation
- Grid-management challenges
- Reduced forecasting reliability

This project addresses these challenges by developing a **weather-aware machine learning model** that estimates future power demand from historical data.

---

## Project Objectives

- Analyse the relationship between weather conditions and electricity consumption.
- Build a regression model for power-demand prediction.
- Prepare usable and high-quality data for machine learning.
- Create time-based and weather-based predictive features.
- Evaluate model performance using regression metrics.
- Compare actual power demand with predicted values.
- Support efficient energy planning through data-driven insights.

---

## Dataset Description

The dataset contains historical power-consumption data combined with weather-related information.

| Data Category | Variables |
|---|---|
| Time-Based Features | Date, hour, day, weekday, month, weekend, season |
| Weather Features | Temperature, humidity, rainfall, wind speed, pressure, cloud cover |
| Energy Features | Historical demand, lag values, rolling averages |
| Target Variable | Electricity demand, power consumption, or energy load |

---

## Data Quality and Usability

The dataset is prepared for regression modelling using the following data-quality practices:

- Removal of duplicate records
- Missing-value identification and treatment
- Date and timestamp standardization
- Numerical data-type validation
- Outlier detection and analysis
- Alignment of weather data with power-demand observations
- Feature scaling where required
- Separation of training and testing datasets

A usable dataset should contain sufficient historical observations, consistent timestamps, valid weather measurements, and a clearly defined electricity-demand target variable.

---

## Data Preprocessing

The preprocessing workflow includes:

1. Loading historical power-consumption and weather data.
2. Inspecting column names, data types, null values, and duplicates.
3. Converting date columns into datetime format.
4. Extracting time-based variables such as hour, weekday, month, and season.
5. Handling missing data using imputation or removal.
6. Identifying unusual observations through outlier analysis.
7. Creating predictive features from historical and weather data.
8. Splitting the dataset into training and testing data.

---

## Feature Engineering

Feature engineering improves model performance by transforming raw data into meaningful predictive variables.

Important engineered features include:

- Hour of the day
- Day of the week
- Weekend indicator
- Month and season
- Peak-hour indicator
- Previous power-demand values
- Lagged energy consumption
- Rolling average demand
- Temperature-based consumption patterns
- Weather interaction variables

These features help the model capture **seasonality**, **demand trends**, **peak-load patterns**, and **weather sensitivity**.

---

## Machine Learning Models

The project evaluates regression algorithms that predict continuous electricity-demand values.

Potential models include:

- Linear Regression
- Ridge Regression
- Decision Tree Regressor
- Random Forest Regressor
- Gradient Boosting Regressor
- XGBoost Regressor

The final model is selected based on forecasting accuracy, error reduction, and generalization performance.

---

## Regression Metrics

Regression metrics measure the difference between actual electricity demand and predicted electricity demand.

### Mean Absolute Error (MAE)

**MAE** measures the average absolute difference between actual and predicted values.

MAE = Average of |Actual Value - Predicted Value|

A lower MAE indicates better average forecasting accuracy.

### Mean Squared Error (MSE)

**MSE** calculates the average squared difference between actual and predicted values.

MSE = Average of (Actual Value - Predicted Value)²

MSE gives higher importance to larger prediction errors.

### Root Mean Squared Error (RMSE)

**RMSE** is the square root of Mean Squared Error.

RMSE = √MSE

RMSE is useful for power forecasting because it strongly penalizes large demand-prediction errors.

### R-Squared Score (R²)

**R² Score** measures the proportion of electricity-demand variation explained by the regression model.

An R² score closer to **1.0** indicates stronger predictive performance.

### Mean Absolute Percentage Error (MAPE)

**MAPE** measures the average prediction error as a percentage.

MAPE provides a practical and easily understandable measure of forecasting accuracy.

---

## Model Evaluation

| Metric | Purpose |
|---|---|
| MAE | Measures average absolute prediction error |
| MSE | Measures squared prediction error |
| RMSE | Highlights large forecasting errors |
| R² Score | Measures explained variation in electricity demand |
| MAPE | Measures average percentage forecasting error |

A strong forecasting model should produce **low MAE**, **low RMSE**, **low MAPE**, and a **high R² score**.

---

## Visual Analysis

The project includes visualizations for exploratory analysis and model validation.

- Historical electricity-demand trends
- Power-consumption distribution
- Weather-variable distributions
- Correlation heatmap
- Actual versus predicted power demand
- Residual-error distribution
- Feature-importance analysis
- Seasonal demand trends
- Peak-load analysis

---

## Project Structure

- `Data/` — Raw and processed datasets
- `Model/` — Trained machine learning models and evaluation results
- `Notebook/` — Data analysis and model-development notebooks
- `Presentation/` — Project presentation materials

---

## Technologies Used

- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Scikit-learn**
- **Jupyter Notebook**

---

## Expected Outcome

This project provides a regression-based electricity-demand forecasting system that can support:

- **Power-demand prediction**
- **Peak-load management**
- **Energy generation planning**
- **Grid optimization**
- **Resource allocation**
- **Operational efficiency**
- **Sustainable energy management**

---

## Future Enhancements

- Real-time weather-data integration
- Interactive forecasting dashboard
- Hyperparameter optimization
- Deep-learning forecasting models
- Automated model retraining
- Real-time prediction deployment
- Model-drift monitoring

---

## Author

**Krish Bhatia**  
**Weather-Aware Power Forecasting**  
**Data Science and Machine Learning Project**
