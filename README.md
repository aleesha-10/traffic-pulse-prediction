# Traffic Pulse Prediction: Time-Series Traffic Forecasting

This project focuses on **short-term traffic flow forecasting** using real-world traffic sensor data from California.  
The goal is to **analyze traffic patterns over time**, compare different modeling approaches, and evaluate how well each model captures **temporal dynamics** such as trends, seasonality, and sudden fluctuations.

Rather than building a single model, this project explores **multiple model families** to understand their strengths, limitations, and practical usefulness for traffic prediction tasks.


## Dataset

### Source
The dataset is derived from **PeMS (Performance Measurement System)** traffic data collected by **Caltrans (California Department of Transportation)**.

A preprocessed version of the data was used for this project, containing:
- Aggregated traffic measurements at **5-minute intervals**
- Traffic speed/flow information from multiple sensors
- Data covering California freeway districts

The dataset is **time-indexed**, making it suitable for time-series forecasting and temporal feature engineering.

> !! Raw data is intentionally excluded from the repository due to size constraints.


## Problem Statement

Traffic congestion has significant economic and social costs.  
Accurate short-term traffic forecasting can help with:
- Congestion management
- Traffic signal optimization
- Urban planning
- Real-time routing systems

This project aims to:
- Predict future traffic flow values
- Compare traditional ML models vs time-series–aware models
- Understand how temporal information improves forecasting accuracy


## Modeling Approach

Instead of relying on a single model, we implemented **one model from each major category**.

### Baseline Machine Learning Models
These models treat the problem as a standard regression task.

- **Ridge Regression**  
  - Linear baseline
  - Helps understand whether traffic patterns are approximately linear

- **Random Forest Regressor**  
  - Tree-based ensemble
  - Captures non-linear relationships but lacks temporal awareness

- **MLP Regressor (Neural Network)**  
  - Learns non-linear feature interactions
  - Requires careful scaling and tuning


### Time-Series–Aware Model (Tree-Based)

- **XGBoost with Lag Features**
  - Uses engineered lag features (previous time steps)
  - Explicitly incorporates temporal dependency
  - Achieved the **best overall performance**

This model demonstrates how adding time-awareness significantly improves forecasting quality.


### Statistical Time-Series Model

- **Prophet**
  - Designed for trend + seasonality modeling
  - Useful for interpretability and decomposition
  - Performed poorly on this dataset, highlighting that:
    - Not all time-series models fit all domains
    - Traffic data contains complex short-term dynamics



### Ensemble Model

- **Weighted Ensemble (XGBoost + Prophet)**
  - Combines predictions from multiple models
  - Demonstrates ensemble forecasting concepts
  - Used primarily for experimentation and comparison



## Model Evaluation

### Metrics Used
- **Mean Squared Error (MSE)**
- **R² Score**

### Key Results Summary

| Model | MSE | R² |
|-----|-----|-----|
| Ridge Regression | ~6.13 | ~0.60 |
| Random Forest | ~6.71 | ~0.57 |
| MLP Regressor | ~6.39 | ~0.59 |
| Time-Series XGBoost | **~6.21** | **~0.60** |
| Prophet | Very high | Negative |
| Ensemble | ~6.96 | ~0.55 |

 **Key Insight:**  
Time-aware XGBoost outperformed other models, showing the importance of temporal feature engineering for traffic forecasting.


## Visualization & Analysis

The project includes:
- Actual vs predicted traffic flow plots
- Time-series forecasts

These plots help interpret **where models succeed or fail**, especially during peak congestion periods.
All the conclusions, interpretations and results have been mentioned in the notebooks. 

