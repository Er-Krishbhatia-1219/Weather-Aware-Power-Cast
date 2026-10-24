# Weather-Aware Power Forecasting

## Executive Summary

**Weather-Aware Power Forecasting** is a time-aware machine learning project that forecasts electricity demand in megawatts (MW) using historical load, meteorological conditions, calendar variables, and lag-based demand signals.

The project transforms high-frequency electricity-demand data into a structured forecasting dataset and evaluates multiple regression models using a strict chronological train-validation-test design. The final linear regression model achieved a **test MAE of 24.59 MW**, **test RMSE of 41.87 MW**, and an **R² score of 0.9991** on 2024 data.

These results demonstrate strong short-term forecasting performance and establish a data-driven framework for energy planning, peak-load management, and operational optimization.

---

## Business Context

Electricity demand is influenced by weather volatility, seasonal cycles, calendar effects, and recent consumption behaviour. Inaccurate demand forecasts can result in:

- Inefficient power generation and dispatch decisions
- Higher balancing and operating costs
- Greater risk during peak-demand periods
- Suboptimal grid-resource allocation
- Reduced reliability in demand planning

This project addresses the problem through **supervised regression modelling**, combining weather indicators with temporal and historical-load features to estimate future electricity demand.

---

## Dataset Profile

The source dataset contains high-frequency electricity-demand and weather observations from **2021 to 2024**.

| Data Characteristic | Value |
|---|---:|
| Initial observations | 393,440 |
| Model-ready observations | 347,745 |
| Modelling period | 8 January 2021 to 11 December 2024 |
| Expected data frequency | 5 minutes |
| Target variable | `Power_Demand_Mw` |
| Target unit | MW |
| Model-ready features | 21 |

The target variable ranges from **1,302.08 MW** to **8,631.53 MW**, with an average demand of **3,960.74 MW**.

---

## Input Features

The forecasting dataset combines weather, time, and historical-demand features.

| Feature Group | Variables |
|---|---|
| Weather Variables | Temperature, dew point, relative humidity, wind speed, wind direction, atmospheric pressure |
| Calendar Variables | Year, month, day, hour, minute, day of week, weekend indicator, Indian public-holiday indicator |
| Historical Demand Variables | 5-minute lag, 1-hour lag, 1-day lag, 1-week lag, previous-hour rolling mean |
| Data-Quality Variable | Missing wind-direction indicator |

### Weather Data Coverage

| Variable | Observed Range |
|---|---|
| Temperature | 4.0°C to 46.4°C |
| Dew Point | -8.6°C to 30.3°C |
| Relative Humidity | 5% to 100% |
| Wind Speed | 0.0 to 63.0 m/s |
| Atmospheric Pressure | 989.6 to 1027.0 mbar |

---

## Data Engineering and Quality Controls

The data-preparation workflow includes:

1. Renaming raw variables into consistent analytical field names.
2. Converting timestamps into a datetime index.
3. Removing irrelevant columns and duplicate analytical fields.
4. Creating a missingness flag for wind-direction values.
5. Forward-filling missing wind-direction observations.
6. Generating calendar features from the timestamp.
7. Creating weekend and India-specific public-holiday indicators.
8. Engineering lag and rolling-mean demand features.
9. Removing records without complete lag history.
10. Preserving chronological order to prevent future data from entering earlier training periods.

The final analytical dataset contains no missing values in the model features.

---

## Feature Engineering

The project uses demand-history features to capture short-term persistence and recurring consumption patterns.

| Engineered Feature | Forecasting Purpose |
|---|---|
| `Demand_Lag_5min` | Captures immediate demand continuity |
| `Demand_Lag_1hr` | Captures intra-day demand behaviour |
| `Demand_Lag_1day` | Captures daily seasonality |
| `Demand_Lag_1week` | Captures weekly consumption cycles |
| `Demand_mean_last_hour` | Smooths short-term demand variation |
| `Is_Weekend` | Captures weekend consumption behaviour |
| `Is_Holiday` | Captures public-holiday effects |
| `Missing_Wind_Drxn_Deg` | Retains information about weather-data completeness |

---

## Modelling Strategy

The project uses a time-based split rather than a random split, ensuring that the model is evaluated on future periods.

| Dataset Split | Period | Purpose |
|---|---|---|
| Training Set | 2021–2022 | Model fitting |
| Validation Set | 2023 | Model selection and comparison |
| Test Set | 2024 | Final out-of-sample evaluation |

The preprocessing pipeline applies:

- Median imputation and standardization to numerical features
- Most-frequent imputation to categorical features
- One-hot encoding for categorical variables
- Unknown-category handling for robust prediction

---

## Models Evaluated

The following models were evaluated on the 2023 validation period:

- Persistence baseline using 1-day lag demand
- Persistence baseline using 5-minute lag demand
- Linear Regression
- Random Forest Regressor
- XGBoost Regressor

---

## Validation Performance

| Model | MAE (MW) | RMSE (MW) | R² Score |
|---|---:|---:|---:|
| 1-Day Lag Baseline | 463.38 | 709.50 | 0.6483 |
| 5-Minute Lag Baseline | 27.34 | 41.25 | 0.9988 |
| **Linear Regression** | **23.48** | **37.84** | **0.9990** |
| Random Forest Regressor | 24.61 | 40.64 | 0.9988 |
| XGBoost Regressor | 26.84 | 58.13 | 0.9976 |

### Validation Insight

**Linear Regression produced the strongest validation performance**, achieving the lowest MAE and RMSE and the highest R² score among the evaluated machine learning models.

Compared with the 5-minute persistence baseline, Linear Regression reduced:

- **MAE by approximately 14.1%**
- **RMSE by approximately 8.3%**

This indicates that the combined weather, calendar, and historical-demand features add measurable predictive value beyond a simple short-term persistence forecast.

---

## Final Test Performance

The final Linear Regression model was trained using the combined 2021–2023 data and evaluated on the unseen 2024 test period.

| Metric | Result | Interpretation |
|---|---:|---|
| **MAE** | **24.59 MW** | Average absolute forecasting error |
| **RMSE** | **41.87 MW** | Error measure with greater sensitivity to larger deviations |
| **R² Score** | **0.9991** | Proportion of demand variation explained by the model |
| 5-Minute Baseline MAE | 29.09 MW | Reference short-term persistence error |
| 5-Minute Baseline RMSE | 45.42 MW | Reference short-term persistence error |

### Test-Set Interpretation

On unseen 2024 data, the final model:

- Reduced **MAE by approximately 15.5%** compared with the 5-minute baseline.
- Reduced **RMSE by approximately 7.8%** compared with the 5-minute baseline.
- Explained approximately **99.91% of the variation** in observed electricity demand.

The model’s strong test performance indicates stable generalization across the final out-of-sample period.

---

## Regression Metrics

### Mean Absolute Error — MAE

MAE measures the average absolute difference between actual and predicted electricity demand.

```text
MAE = Average of |Actual Demand - Predicted Demand|
```

MAE is expressed in **MW**, making it directly interpretable for energy operations.

### Root Mean Squared Error — RMSE

RMSE measures the square root of average squared forecast error.

```text
RMSE = √Mean Squared Error
```

RMSE gives greater weight to large prediction errors, which is useful when substantial load deviations create operational risk.

### R-Squared Score — R²

R² measures the proportion of demand variability explained by the model.

```text
R² = 1 - (Residual Sum of Squares / Total Sum of Squares)
```

An R² score close to 1 indicates that the model closely follows observed demand variation.

---

## Analytical Visualizations

The notebook includes visual analysis for both data understanding and model validation:

- Monthly power-demand analysis
- Yearly power-demand trend analysis
- Daily electricity-demand time series
- Demand distribution by month
- Temperature versus power-demand analysis
- Dew point versus power-demand analysis
- Hourly power-demand analysis
- Wind-direction demand comparison
- Humidity versus power-demand analysis
- Correlation heatmap
- Actual versus predicted demand comparison
- Forecast-error analysis by hour
- Daily-average actual versus predicted demand for 2024

---

## Project Structure

```text
Weather-Aware-Power-Cast/
│
├── Data/
│   └── Power_Demand_2021-2024.csv
│
├── Model/
│   └── Electricity Demand Forcasting Model.pkl
│
├── Notebook/
│   └── Weather Aware Power Cast.ipynb
│
├── Presentation/
│
└── README.md
```

---

## Technology Stack

- **Python**
- **Pandas** — data manipulation and time-series processing
- **NumPy** — numerical computation
- **Matplotlib** — data visualization
- **Seaborn** — statistical visualization
- **Scikit-learn** — preprocessing, pipelines, regression, and evaluation
- **XGBoost** — gradient-boosting regression
- **Joblib** — model serialization
- **Holidays** — India public-holiday feature generation
- **Jupyter Notebook** — exploratory analysis and model development

---

## Practical Value

This forecasting solution can support:

- Electricity-demand planning
- Short-term load forecasting
- Peak-demand monitoring
- Energy procurement decisions
- Grid balancing
- Resource optimization
- Weather-sensitive demand analysis
- Operational risk reduction

---

## Future Enhancements

- Integrate real-time weather data from an API
- Build an interactive forecasting dashboard
- Add probabilistic forecasting intervals
- Perform hyperparameter optimization
- Evaluate advanced time-series models
- Deploy the model as a web application
- Monitor data drift and forecast performance in production

---

## Author

**Krish Bhatia**  
**Weather-Aware Power Forecasting**  
**Data Science and Machine Learning Project**
