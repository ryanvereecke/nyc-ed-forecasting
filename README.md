# NYC Emergency Department Visit Forecasting

This project builds a complete data science workflow to analyze and forecast daily emergency department (ED) visit volumes in New York City. The analysis integrates hospital utilization data, influenza-like illness (ILI) activity, weather features, and calendar effects to identify key drivers of ED demand and evaluate predictive performance across several machine-learning models.

---

## Project Objectives
- Understand which factors most strongly influence daily ED visit volumes.
- Build a reproducible data pipeline for cleaning, merging, and engineering features.
- Compare baseline and advanced machine learning models for forecasting accuracy.
- Quantify the predictive value of illness activity, weather, and temporal patterns.
- Produce interpretable insights and visualizations to guide real-world planning.

---

## Data Sources
This project uses four primary datasets:

### **1. NYC Health ED Visits**
Contains daily ED visit totals, influenza-like illness (ILI) visits, pneumonia visits, and admissions.

### **2. Influenza/Pneumonia Activity**
Daily influenza-like illness (ILI) activity metrics used to capture community disease burden.

### **3. Weather Data (Meteostat)**
Includes:
- Average, minimum, maximum temperature  
- Precipitation  
- Wind speed  
- Atmospheric pressure  

### **4. Calendar Features**
Automatically generated:
- Day of week  
- Weekend flag  
- Month  
- Year  
- Week of year  
- Holiday indicator  

> **Note:** Raw datasets contain ~82 million rows before aggregation.  
Final cleaned dataset contains ~600 daily records.

---

## Data Cleaning & Feature Engineering
The data pipeline includes:

- Standardizing column formats across datasets  
- Dropping incomplete or duplicated entries  
- Merging ED, weather, and illness activity datasets  
- Creating predictive features:
  - **Lag features**: `ili_lag1`, `ili_lag7`
  - **Rolling averages**: `ili_7d_avg`
  - **Calendar indicators**
- Encoding weekends and holidays  
- Filtering extreme or inconsistent values  
- Ensuring proper data types (numeric, boolean, categorical)

---

## Exploratory Data Analysis (EDA)
Key analysis steps include:

- Descriptive statistics  
- Time-series plots and trend visualization  
- Pearson & Spearman correlation heatmaps  
- Seasonal patterns and weekly cycles  
- Checking for anomalies and outliers  
- Identifying the strongest predictors of ED volume  

**Finding:** ILI activity and autoregressive features (lags, rolling averages) consistently show the strongest relationship with ED visits.

---

## Models Implemented

### **1. Linear Regression (Baseline)**
- High interpretability  
- Strong predictive baseline  
- Performed best overall  
- **R² ≈ 0.70**

### **2. Random Forest Regression**
- Captures nonlinear interactions  
- Robust to noise  
- Slightly underperforms LR  
- Tends to **underpredict extreme high-visit days**

### **3. Gradient Boosting Regression**
- More complex ensemble model  
- Strong performance but similar limitations to RF  
- Does not improve prediction of extreme spikes

---

## Model Performance Summary

| Model                 | R²     | RMSE | MAE |
|-----------------------|--------|------|-----|
| **Linear Regression** | ~0.705 | ~29  | ~22 |
| **Random Forest**     | ~0.689 | ~30  | ~21 |
| **Gradient Boosting** | Similar to RF | — | — |

**Key takeaway:**  
Illness activity + lag features explain the majority of daily ED visit variation.  
Weather and calendar factors show smaller but consistent secondary effects.

---

## Repository Structure

