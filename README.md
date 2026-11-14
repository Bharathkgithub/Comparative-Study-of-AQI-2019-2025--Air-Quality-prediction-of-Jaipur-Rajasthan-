# Comparative-Study-of-AQI-2019-2025--Air-Quality-prediction-of-Jaipur-Rajasthan-
Machine Learning-based Air Quality Analysis and Prediction for Jaipur, Rajasthan (2019–2025) using Python, Linear Regression and Artificial Neural Networks (ANN).

# Jaipur Air Quality (AQI) Analysis & Forecasting, 2019–2025

Statistical and machine-learning analysis of how meteorology drives air pollution in Jaipur, Rajasthan, with a 7-day forecast of PM2.5 and PM10 using an Artificial Neural Network (ANN) compared against a Linear Regression baseline.

Project by **Team 14** for the IISc Centre for Continuing Education online course *From Data to Decisions: Machine Learning & AI for Real-World Science & Engineering* (October 2025).

## Team

Ramu T N · Bharath K · Venisetty Chandrakanth · Ajay Kumar Borah · Kannadhasan S

## Objectives

1. Quantify the relationship between AQI / pollutant concentrations and meteorological variables (wind speed, temperature, humidity, rainfall).
2. Identify seasonal and annual patterns, including the COVID-19 lockdown (2020) and Diwali / crop-burning peaks.
3. Build ML models that forecast PM2.5 and PM10 seven days ahead.
4. Compare a linear baseline with a neural network.

## Data

| Item | Detail |
|---|---|
| Pollutants | AQI, PM2.5, PM10, NO2, SO2, O3, CO (plus NH3, NO, NOx in the notebook) |
| Meteorology | Temperature, relative humidity, wind speed / direction, rainfall, pressure, solar radiation |
| Sources | CPCB (NAMP / AQI bulletin archive), validated against NASA POWER |
| Period / frequency | 2019–2025, daily |
| Station | Police Commissionerate, Jaipur (RSPCB) |

The cleaned daily dataset is included as [`data/cleaned_station_daily_with_AQI.csv`](data/cleaned_station_daily_with_AQI.csv) (about 2,400 daily rows). See [`data/README.md`](data/README.md).

## Method

1. **Preprocessing**: interpolate missing values, align pollutant and weather data by date, drop records with excessive gaps, scale features.
2. **EDA**: time-series plots, seasonal boxplots, Pearson and Spearman correlation heatmaps, event annotations.
3. **Baseline**: OLS / Linear Regression of each pollutant on wind, temperature, RH and rainfall.
4. **ANN**: inputs are meteorological variables, other pollutants, temporal features and lagged values; trained with backpropagation and early stopping.
5. **Evaluation**: R² and RMSE (MAE in the notebook); AQI mapped to CPCB categories (Good to Severe).

## Key findings

- Strong seasonality: winter (Dec–Feb) is worst, monsoon is cleanest.
- Wind speed and rainfall are negatively correlated with PM2.5 / PM10; humidity shows a moderate positive relationship; temperature is mixed.
- Linear Regression: R² ≈ 0.5–0.6, underpredicts peaks.
- ANN: R² ≈ 0.80–0.90 in the report (R² 0.81, RMSE 12.7 µg/m³ for PM2.5 in the slides).

## Repository structure

```
jaipur-aqi-forecasting/
├── notebooks/
│   └── EDA_G14.ipynb          # EDA → regression → ANN → 7-day forecast
├── docs/
│   ├── IISC_AQI_project_Final.pdf       # project report
│   └── IISE_bangalore_Group_14.pptx     # presentation
├── data/
│   └── cleaned_station_daily_with_AQI.csv   # cleaned daily dataset
├── results/                   # generated figures and 7-day prediction CSVs
├── requirements.txt
├── .gitignore
└── README.md
```

## Getting started

```bash
git clone https://github.com/YOUR_USERNAME/jaipur-aqi-forecasting.git
cd jaipur-aqi-forecasting
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/EDA_G14.ipynb
```

The dataset is included in `data/`, and the notebook loads it by relative path, so no cloud drive access is needed.

## Limitations and future work

- Missing or inconsistent CPCB data; single-station measurements may not represent the whole city.
- Extreme events (lockdown, Diwali, crop burning) are hard for models to capture.
- Next steps: satellite AOD (MODIS), multi-station / multi-city comparison, a real-time forecasting dashboard, linking forecasts to health data.

## Acknowledgements

Data from the Central Pollution Control Board (CPCB) and NASA POWER. Course: IISc Centre for Continuing Education, Bengaluru.
