

### IDS705 Final Project - Prairie Dog Team

# 🌎 Modeling Short-Term Electricity Prices in ERCOT  

- Jessalyn Chuang, Neha Manish Shah, Michelle Schultze, Zixiao Tan

## Project Overview

**Title:** Modeling Short-Term Electricity Prices in ERCOT  
**Objective:** Forecast short-term electricity prices across different time horizons (1-hour, 1-day, 1-week ahead) using machine learning and deep learning models, based solely on publicly available data.

## Abstract

This project explores how open-access data can be leveraged to forecast electricity prices in the ERCOT market. We compare tree-based models (XGBoost, LightGBM) with deep learning models (LSTM, GRU) for multiple forecasting horizons. Rolling-origin resampling and a time-aware train-validation-test split strategy ensure temporal integrity. LightGBM achieves the best performance for 1-hour ahead forecasts, while LSTM and GRU models slightly outperform in 1-day ahead forecasts. Lagged prices and regional temperatures emerge as the most important predictors. Our results highlight that accessible data and interpretable models can provide accurate and actionable price forecasts, supporting more transparent and adaptive electricity markets.


## Table of Contents

- [Introduction](#introduction)
- [Background](#background)
- [Data](#data)
- [Methodology](#methodology)
- [Experiments](#experiments)
- [Conclusion](#conclusion)
- [Presentation](#presentation)
- [Repository Structure](#repository-structure)
- [Usage Instructions](#usage-instructions)

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

## Repository Structure

```python
.
├── LICENSE                     # Open-source license for the project
├── README.md                   # Overview and instructions
├── requirements.txt            # Python package dependencies
├── structure.txt               # Description of directory structure
├── test.txt                    # (Optional) Test notes or placeholder
├── .gitignore                  # Git ignore rules
├── .DS_Store                   # (MacOS system file, can be deleted)
│
├── .github/
│   └── workflows/
│       └── repo_checks.yml     # GitHub Actions for notebook rendering and checks
│
├── data/
│   ├── 01_raw/                 # Raw datasets
│   │   ├── Henry_Hub_Natural_Gas_Spot_Price.csv
│   │   ├── Henry_Hub_Natural_Gas_Spot_Price_updated.csv
│   │   └── wet_bulb_temp.xlsx
│   │
│   └── 02_processed/           # Cleaned and feature-engineered datasets
│       ├── all_hourly_data.csv
│       └── all_hourly_data_v2.csv
│
├── figures/                    # All generated plots and visualizations
│   ├── 01_LMP_OverTime.png
│   ├── 02_ACF_lmp_HB_BUSAVG.png
│   ├── 03_PACF_lmp_HB_BUSAVG.png
│   ├── 04_Correlation_Matrix.png
│   ├── 05_gini_gain_importance.png
│   ├── 06_permutation_importance.png
│   ├── 07_3D_Hyperparameter_Search_Results.png
│   ├── 08_3D_Hyperparameter_Search_Results_2.png
│   ├── 09_TrainVal_Split.png
│   ├── 10_Rolls_Origin1.png
│   ├── 11_Rolls_Origin2.png
│   ├── 12_Rolls_Origin3.png
│   ├── 13_Final_Train.png
│   └── 14_Blocked_CV.png
│
└── notebooks/                  # Jupyter notebooks for analysis and modeling
    ├── 01_Data_Scrape.ipynb                # Data collection and preprocessing
    ├── 02_Experiments_DecisionTrees.ipynb  # Initial tree-based experiments
    ├── 03_Experiments_Xgboost.ipynb        # XGBoost model tuning and evaluation
    └── 04_Final_model.ipynb                # Final model training, testing, and performance comparison

```


- **`data/01_raw/`**: Raw datasets including Henry Hub natural gas spot prices and Plano wet bulb temperature from GridStatus.io, EIA, and local weather sources.
- **`data/02_processed/`**: Feature-engineered datasets with lag variables, target shifts, and time-aggregated data used in model training.
- **`notebooks/`**: Jupyter Notebooks for data scraping (`01_Data_Scrape.ipynb`), model experimentation (tree-based and deep learning), and final model evaluation.
- **`figures/`**: Visualizations and diagnostic plots including ACF/PACF, feature importance, training-validation split diagrams, and hyperparameter search results.
- **`.github/workflows/`**: GitHub Actions YAML file for automating notebook rendering and reproducibility checks.
- **`README.md`**: Overview of the project, including its purpose, structure, and instructions for navigating the repository.
- **`requirements.txt`**: Python dependencies required to run the project (for reproducibility).


### Usage Instructions

1. **Setup**  
   Clone the repository and install all dependencies listed in `requirements.txt`:
   ```bash
   git clone git@github.com:YourUsername/IDS705_Final_Project.git
   cd IDS705_Final_Project
   pip install -r requirements.txt
   ```

2. **Data Preparation**  
   - Start with `01_Data_Scrape.ipynb` to fetch and preprocess raw data from GridStatus.io, EIA, and local weather sources.
   - Use `all_hourly_data_v2.csv` from `data/02_processed/` as the final training-ready dataset.

3. **Modeling**
   - Use `04_Final_model.ipynb` to train and evaluate final models (XGBoost, LightGBM, LSTM, GRU) using rolling-origin cross-validation.

4. **Evaluation and Results**  
   - Performance metrics (MAE, RMSE, MAPE) and feature importance are generated and stored in the `results/` folder.
   - Visualizations including autocorrelation, CV strategy, and model importance can be found in the `figures/` directory.


## Presentation

- [Project Presentation Slides](#) *(link to slides if available)*


📄 **Final Report:**  
[View the final report on Google Docs](https://docs.google.com/document/d/1FfgGZznpnw8yCLnL-URstudEnARD1K29jHdmqV0_qN4/edit?usp=sharing)