

### IDS705 Final Project - Prairie Dog Team

# 🌎 Modeling Short-Term Electricity Prices in ERCOT  

- Jessalyn Chuang, Neha Manish Shah, Michelle Schultze, Zixiao Tan

## Project Overview

**Title:** Modeling Short-Term Electricity Prices in ERCOT  
**Objective:** Forecast short-term electricity prices across different time horizons (1-hour, 1-day, 1-week ahead) using machine learning and deep learning models, based solely on publicly available data.

## Abstract

This project explores how open-access data can be leveraged to forecast electricity prices in the ERCOT market. We compare tree-based models (XGBoost, LightGBM) with deep learning models (LSTM, GRU) for multiple forecasting horizons. Rolling-origin resampling and a time-aware train-validation-test split strategy ensure temporal integrity. LightGBM achieves the best performance for 1-hour ahead forecasts, while LSTM and GRU models slightly outperform in 1-day ahead forecasts. Lagged prices and regional temperatures emerge as the most important predictors. Our results highlight that accessible data and interpretable models can provide accurate and actionable price forecasts, supporting more transparent and adaptive electricity markets.

## Repository Structure

- **data/00_raw/**: Original datasets obtained from GridStatus.io, EIA, and local weather records.
- **data/01_processed/**: Preprocessed datasets, including feature engineering like lag variables and scaling.
- **notebooks/**: Jupyter Notebooks for exploratory data analysis, model training, evaluation, and result visualization.
- **models/**: Saved model objects (trained XGBoost, LightGBM, LSTM, and GRU models).
- **results/**: Evaluation results including MAE, RMSE metrics, and feature importance plots.
- **README.md**: Project overview, methodology, repository structure, and navigation guide.

## Table of Contents

- [Introduction](#introduction)
- [Background](#background)
- [Data](#data)
- [Methodology](#methodology)
- [Experiments](#experiments)
- [Conclusion](#conclusion)
- [Presentation](#presentation)

## Introduction

Understanding short-term electricity price movements is crucial for ensuring grid stability, market efficiency, and energy equity. This project aims to build replicable, flexible, and interpretable forecasting models using publicly accessible data.

## Background

Electricity prices are highly nonlinear, volatile, and influenced by weather, load, fuel mix, and policy changes. Traditional models like ARIMA struggle with these complexities, leading to increased adoption of machine learning and deep learning approaches. However, many existing models rely on proprietary data. We address the gap by testing forecasting performance with only open-access datasets.

## Data

The datasets are sourced from GridStatus.io, EIA, and Plano, Texas weather stations, covering 2018–2025. Features include real-time load, generation fuel mix, solar generation, regional temperatures, wet bulb temperature, and Henry Hub natural gas spot prices. The target variable is the ERCOT Average Hub Real-Time LMP (Locational Marginal Price).

## Methodology

We forecast 1-hour, 1-day, and 1-week ahead prices using:
- **XGBoost** and **LightGBM** for structured, tabular modeling.
- **LSTM** and **GRU** networks for sequential deep learning.
Rolling-origin resampling is used for cross-validation, and hyperparameters for tree-based models are optimized using **Optuna**. Feature importance is evaluated via permutation importance to maintain consistency across model types.

## Experiments

### Model Development
- Separate models were trained for each prediction horizon.
- Evaluation metrics include **MAE**, **RMSE**, and **MAPE**.
- Feature engineering emphasized lagged price variables, weather features, and load information.

### Interpretability
- SHAP values for tree models.
- Permutation importance and attention-based analysis for LSTM and GRU.

## Conclusion

Tree-based models (especially LightGBM) perform best for short-term (1-hour) forecasts. Deep learning models (LSTM, GRU) show improved performance at longer horizons (1-day). Lagged prices and temperature features are the strongest predictors across all models. Publicly available data, when combined with machine learning, can yield robust and interpretable price forecasts, supporting broader energy market participation.

## Presentation

- [Project Presentation Slides](#) *(link to slides if available)*

---
# IDS 705 Final Project
Team Prairie Dog! (#13) 

📄 **Final Report:**  
[View the final report on Google Docs](https://docs.google.com/document/d/1FfgGZznpnw8yCLnL-URstudEnARD1K29jHdmqV0_qN4/edit?usp=sharing)