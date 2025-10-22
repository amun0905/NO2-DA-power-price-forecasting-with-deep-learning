# Forecasting Day-ahead Electricity Prices in the Norwegian NO2 Bidding Zone using Deep Learning

This repository contains code for forecasting NO2 Day-ahead power prices using publicly available data from ENTSO-E and Open-Meteo, with deep learning models.

---

## Project Overview

This project compares traditional machine learning and deep learning approaches to capture complex, nonlinear, and temporal relationships in market data.

**Workflow:**
- Construct a multivariate time series dataset from public APIs  
- Implement and train multiple deep learning architectures  
- Evaluate and compare forecasting accuracy using multiple performance metrics  

---

## Data Sources

The dataset was built using data collected from ENTSO-E Transparency Platform and Open-Meteo API.

### **ENTSO-E Data**
- **Load Forecasts:** For NO2 and neighboring zones (NO1, NO5, DK, NL, DE_LU)  
- **Net Transfer Capacities (NTC):** Week-ahead capacities between zones  
- **Hydropower Reservoir Levels:** Weekly reservoir data for NO2  

### **Open-Meteo Weather Data**
Representative cities were selected for each bidding zone:
| Zone | City | Coordinates |
|------|------|--------------|
| NO1 | Oslo | (59.9127, 10.7461) |
| NO2 | Kristiansand | (58.1467, 7.9956) |
| NO5 | Bergen | (60.3930, 5.3242) |
| DK | Aalborg | (57.0480, 9.9187) |
| NL | Rotterdam | (51.9225, 4.4792) |
| DE_LU | Kiel | (54.3213, 10.1349) |

**Weather Variables:**
- Temperature (°C)  
- Total Cloud Cover (%)  
- Wind Speed (m/s at 80m)  

All data were resampled to an hourly resolution (October 2023 – March 2025). Weekly data such as hydropower levels were forward-filled to maintain temporal alignment.

---

## Models Implemented

| Model | Type | Framework |
|--------|------|------------|
| XGBoost | Baseline ML (Ensemble Trees) | `xgboost` |
| Vanilla RNN | Recurrent Neural Network | `TensorFlow / Keras` |
| LSTM | Long Short-Term Memory | `TensorFlow / Keras` |
| GRU | Gated Recurrent Unit | `TensorFlow / Keras` |
| TCN | Temporal Convolutional Network | `TensorFlow / Keras` |

All deep learning models predict day-ahead prices 24 hours ahead, using historical sequences as input.  
Regularization methods such as dropout and L2 penalties were applied to prevent overfitting.  
Hyperparameters (e.g., learning rate, sequence length, batch size) were tuned using time-series cross-validation.

---

## Model Performance

| Model | MAE | RMSE | R² | Adjusted R² | MAPE | DA |
|--------|-----|------|----|--------------|------|----|
| XGBoost | 10.80 | 34.15 | 0.66 | 0.65 | 14.83% | 67.44% |
| Vanilla RNN | 9.73 | 19.84 | 0.88 | 0.88 | 18.01% | 70.05% |
| LSTM | 10.79 | 20.44 | 0.87 | 0.88 | 18.66% | 68.32% |
| GRU | 9.69 | 20.65 | 0.87 | 0.87 | 18.21% | 69.51% |
| TCN | 12.42 | 20.96 | 0.87 | 0.87 | 25.44% | 67.52% |

> Best Model: Vanilla RNN — highest accuracy, best generalisation, and stable directional prediction.  
> Runner-up: GRU — comparable performance with fewer parameters and faster training.

---

## Insights

- Deep learning architectures significantly outperform XGBoost in all metrics.  
- Vanilla RNN offers the best performance — proving that simpler architectures can generalize better on moderate-sized datasets.  
- GRU achieves near-equivalent accuracy with fewer parameters.  
- LSTM struggled with overfitting on limited data, while TCN tended to overestimate prices during volatility peaks.  
- Residual analysis showed mild heteroskedasticity and greater variance during high-price periods.
