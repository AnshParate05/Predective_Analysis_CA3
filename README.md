# Electricity Load Forecasting for Smart Buildings Using Machine Learning

## Project Overview

This project demonstrates an end-to-end predictive analytics workflow for forecasting near-future appliance electricity consumption using machine learning regression techniques.

The implementation uses the **UCI Appliances Energy Prediction dataset**. It explores historical energy readings, time-related variables, and environmental measurements to predict the next appliance energy reading at a 10-minute interval. Model performance is assessed by comparing actual and predicted values and calculating regression evaluation metrics.

> **Scope note:** The dataset represents appliance energy use in a monitored home. The project is therefore a smart-home energy forecasting prototype, rather than a validation study across multiple commercial buildings.

## Problem Statement

Electricity consumption changes with appliance activity, time of day, and environmental conditions. The objective is to build a predictive model that estimates the next 10-minute appliance energy reading from available historical and contextual features.

## Objectives

- Understand and explore the electricity consumption dataset.
- Prepare and preprocess data for predictive modelling.
- Create time-based and historical features.
- Split the observations chronologically to reflect a forecasting scenario.
- Train and compare regression models.
- Evaluate predictions using R², Mean Absolute Error (MAE), and Root Mean Squared Error (RMSE).
- Visualize actual versus predicted energy consumption and interpret model errors.

## Dataset

**Name:** Appliances Energy Prediction  
**Source:** UCI Machine Learning Repository  
**Dataset page:** https://archive.ics.uci.edu/dataset/374/appliances+energy+prediction

The original dataset contains 19,735 observations recorded at 10-minute intervals, with 29 columns including the timestamp. Variables include appliance energy consumption, lighting, indoor temperature and humidity, and weather-related measurements.

### Target

The notebook creates a next-step target by shifting the `Appliances` reading by one row. Since each row is spaced 10 minutes apart, this represents the next 10-minute reading.

### Example features

Depending on the notebook's feature selection, predictors can include:

- Current appliance energy consumption and historical readings
- Indoor and outdoor temperature and humidity
- Lighting
- Time-based features such as hour, weekday, and weekend indicator

## Methodology / KDD Workflow

The project follows these stages:

1. **Problem identification** — define the electricity forecasting objective.
2. **Data collection** — load the UCI dataset.
3. **Data understanding and EDA** — inspect dimensions, data types, distributions, correlations, and patterns.
4. **Data preprocessing** — inspect missing values, duplicates, and timestamp ordering.
5. **Feature engineering** — derive time-related and historical features.
6. **Data transformation** — prepare the selected predictors for model training as required.
7. **Chronological data splitting** — separate training, validation, and test periods without random shuffling.
8. **Model training** — evaluate regression approaches such as Linear Regression, Random Forest, Extra Trees, and Gradient Boosting variants where implemented.
9. **Model selection and evaluation** — use validation results to select a model and evaluate final performance on held-out test observations.
10. **Interpretation** — inspect Actual vs. Predicted plots and regression metrics.

## Evaluation Metrics

- **R² (coefficient of determination):** measures how well predictions explain variation in the observed target relative to a mean-prediction baseline.
- **MAE (Mean Absolute Error):** average absolute difference between actual and predicted values.
- **RMSE (Root Mean Squared Error):** square root of the average squared prediction error; more sensitive to large errors than MAE.

### Current reported result

The uploaded notebook reports the following test-set results for its Gradient Boosting regression model:

| Metric | Reported value |
|---|---:|
| R² | 0.5604 |
| MAE | 26.4412 Wh |
| RMSE | 60.2582 Wh |

These values describe the current notebook run and should be updated if the model or evaluation procedure changes. R² is a regression metric and should not be described as classification accuracy. The current result is a baseline for improvement and does not meet an R² target above 0.93.

## Actual vs. Predicted Visualization

The notebook visualizes model predictions against observed values. A close match between actual and predicted values indicates better forecasting performance. Residuals, calculated as `actual - predicted`, can help identify systematic overprediction, underprediction, and unusually large errors.

## Repository Structure

A suggested GitHub repository layout is:

```text
electricity-load-forecasting/
├── README.md
├── PA_CA3_Ansh.ipynb
├── energydata_complete.csv
└── results/
    ├── actual_vs_predicted.png
    └── model_comparison.csv
```

Adjust filenames and include the `results/` files only if they exist in your repository. If the dataset file is too large or its redistribution is restricted, provide the official dataset link instead of committing the raw file.

## Requirements

The notebook uses Python and common data science libraries. Install the libraries required by the notebook:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

If additional libraries are imported in the notebook, install those as well.

## How to Run

1. Clone or download this repository.
2. Download the dataset from the [UCI dataset page](https://archive.ics.uci.edu/dataset/374/appliances+energy+prediction) if it is not included.
3. Place `energydata_complete.csv` in the location expected by the notebook, or update the file path in the data-loading cell.
4. Open the notebook in Jupyter Notebook, JupyterLab, or Google Colab.
5. Run the cells in order, from data loading and exploration through modelling and evaluation.
6. Review the regression metrics and Actual vs. Predicted visualization produced by the notebook.

## Important Methodological Notes

- Keep the observations in chronological order for forecasting evaluation.
- Fit preprocessing transformations only on training data, then apply them to validation and test data.
- Build lag and rolling-window features using past information only. Avoid backfilling features with future observations.
- Use the validation period for model selection and keep the test period untouched until final evaluation.
- Do not claim a particular performance target unless it is supported by the final held-out test results.

## Limitations and Future Improvements

- The dataset represents one monitored home, which limits conclusions about different buildings.
- Sudden changes in appliance use can be difficult to forecast.
- Performance can be improved by validating feature engineering, comparing models using chronological validation, tuning hyperparameters, and analysing errors across time periods.
- Further evaluation on datasets from additional buildings would be needed to assess generalization to commercial smart buildings.

## References

1. Candanedo, L. M., Feldheim, V., & Deramaix, D. (2017). *Data driven prediction models of energy use of appliances in a low-energy house*. Energy and Buildings, 140, 81–97.
2. UCI Machine Learning Repository. *Appliances Energy Prediction*. https://archive.ics.uci.edu/dataset/374/appliances+energy+prediction

## Author

**Ansh Parate**
