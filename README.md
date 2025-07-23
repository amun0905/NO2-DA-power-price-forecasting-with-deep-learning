# Forecasting Day-Ahead Electricity Prices in Norwegian NO2 Bidding Zone Using Deep Learning

This project explores the use of deep learning models to forecast day-ahead electricity prices in Norway's NO2 bidding zone—a region with a highly renewable, hydro-dominated power system. The goal is to improve prediction accuracy in a volatile and interconnected market by comparing advanced machine learning and deep learning models.

## Project Overview

Day-ahead price forecasting plays a critical role in energy trading, planning, and grid stability. This study applies and compares several models, including:
- XGBoost (Baseline)
- Recurrent Neural Network (RNN)
- Long Short-Term Memory (LSTM)
- Gated Recurrent Unit (GRU)
- Temporal Convolutional Network (TCN)

The models are evaluated using a comprehensive set of error metrics, including R², MAE, RMSE, MAPE, and Directional Accuracy.

## Dataset

Data was collected from the following sources:
- **ENTSO-E Transparency Platform**: Load forecasts, Net Transfer Capacities (NTC), hydropower reservoir levels
- **Open-Meteo API**: Hourly weather forecasts (temperature, wind speed, cloud cover)
- **Time Period**: October 2023 – March 2025
- **Resolution**: Hourly data

Each bidding zone (e.g., NO1, NO2, DK, DE_LU) was matched with a representative geographic location to collect weather features.

## Models & Methods

### Baseline:
- **XGBoost** – A tree-based model offering strong baseline performance.

### Deep Learning Models:
- **Vanilla RNN** – Simple recurrent structure, best performing overall.
- **LSTM** – Designed for long-term dependencies but prone to overfitting.
- **GRU** – Balanced accuracy and efficiency.
- **TCN** – Convolution-based model for parallel sequence learning.

All models were built using **TensorFlow (Keras API)** and trained with regularisation (dropout, L2), early stopping, and hyperparameter tuning.

## Evaluation Metrics

| Model      | MAE     | RMSE    | R²     | MAPE   | DA (%) |
|------------|---------|---------|--------|--------|--------|
| XGBoost    | 10.80   | 34.15   | 0.66   | 14.83% | 67.44  |
| RNN        | 9.73    | 19.84   | 0.88   | 18.01% | 70.05  |
| LSTM       | 10.79   | 20.44   | 0.87   | 18.66% | 68.32  |
| GRU        | 9.69    | 20.65   | 0.87   | 18.21% | 69.51  |
| TCN        | 12.42   | 20.96   | 0.87   | 25.44% | 67.52  |

 **Best Performing Model**: Vanilla RNN  
**Observation**: Simpler architectures like RNNs and GRUs performed better than LSTMs and TCNs in this context.


