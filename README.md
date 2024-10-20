# Time Series Analysis and Forecasting Project

## Overview

This project focuses on time series analysis and forecasting using the ARIMA (AutoRegressive Integrated Moving Average) model. It explores data preprocessing, stationarity testing, ARIMA model selection, validation, and finally, forecasting future values. The project uses real-world time series data (monthly index values) to demonstrate the complete process, including model selection based on **AIC** and **BIC** criteria and evaluating the best model for forecasting.

## Key Objectives

1. **Data Preparation**: Load, clean, and preprocess the data for time series analysis.
2. **Stationarity Tests**: Apply unit root tests (ADF, KPSS, Phillips-Perron) to assess stationarity and transform the series if necessary.
3. **ARIMA Model Selection**: Select the best ARIMA model based on AIC/BIC scores using automated procedures.
4. **Forecasting**: Use the selected ARIMA model to forecast future values and compare predicted values with actual future points.
5. **Model Diagnostics**: Evaluate model residuals for autocorrelation, test causality, and validate AR and MA roots.

## Project Structure

### 1. **Data Loading and Preprocessing**
   - **Data Source**: The dataset is loaded from a CSV file containing monthly index values starting from 1990 to 2024.
   - **Data Cleaning**: The last two months of data are separated for future prediction validation. The dataset is converted to time series format using the `zoo` package for handling date-indexed data.
   
   **Key Steps**:
   - Load the dataset and inspect its structure.
   - Prepare the main time series (`data1`) and future validation set (`data2`).
   - Create time series objects using `zoo` with monthly frequency.

### 2. **Stationarity Tests and Differencing**
   - **Stationarity Check**: The Augmented Dickey-Fuller (ADF) test, along with autocorrelation (ACF) and partial autocorrelation (PACF), are used to assess whether the series is stationary.
   - **Differencing**: If the series is not stationary, it is differenced to make it stationary for ARIMA modeling.

   **Tests Used**:
   - ADF Test (`adfTest`)
   - KPSS Test (`kpss.test`)
   - Phillips-Perron Test (`pp.test`)
   - ACF and PACF plots to visually inspect stationarity.

### 3. **ARIMA Model Selection**
   - **Model Estimation**: The ARIMA models are fitted with various combinations of AR (p) and MA (q) orders. A function is used to automatically test all combinations of ARIMA models within specified limits (`pmax=8`, `qmax=2`).
   - **Model Validation**: Models are validated based on statistical significance and the Ljung-Box test for residual autocorrelation.
   - **Model Selection**: The best model is selected based on **AIC** and **BIC** values.

   **Functions Used**:
   - `modelchoice()`: Fits and validates ARIMA models.
   - `armamodelchoice()`: Automates the selection of ARIMA models.
   - **Best Models**: The model with the lowest AIC/BIC is chosen for further analysis.

### 4. **Model Diagnostics**
   - **Residual Analysis**: The residuals of the selected ARIMA model are analyzed to ensure no autocorrelation exists.
   - **Causality Check**: The AR coefficients are checked to ensure the model is causal (i.e., roots lie outside the unit circle).
   - **Inverse Roots Plot**: The inverse roots of AR and MA polynomials are plotted to further verify the model’s stability.

### 5. **Forecasting**
   - **Forecasting Future Values**: Using the best ARIMA model, future values of the time series are forecasted.
   - **Comparison with Actual Values**: The predicted values are compared against the actual future points in the validation dataset (`data2`).
   - **Residual Forecasting**: Forecasts for the differenced series are also performed for comparison.

   **Visualization**:
   - Forecast results are plotted to show the predicted values along with actual future points.
   - Confidence intervals are shown to illustrate the uncertainty in the predictions.

### 6. **Model Evaluation**
   - **Ljung-Box Test**: Perform the Ljung-Box test to check for any remaining autocorrelation in the residuals of the best model.
   - **Plot of Ljung-Box Test Results**: The p-values for each lag are plotted, with a reference line to indicate significant autocorrelations.

## Installation and Dependencies

### Required Packages

The project uses the following R packages for data manipulation, time series analysis, and plotting:
- `zoo`
- `tseries`
- `fUnitRoots`
- `polynom`
- `forecast`
- `car`
- `ellipse`
- `readr`
- `dplyr`
- `lubridate`
- `ggplot2`

To install these dependencies, run the following in your R environment:
```R
required_packages <- c("zoo", "tseries", "fUnitRoots", "polynom", "forecast", "car", "ellipse", "readr", "dplyr", "lubridate", "ggplot2")
install_packages <- function(packages) {
  for (package in packages) {
    if (!require(package, character.only = TRUE)) {
      install.packages(package, dependencies = TRUE)
      library(package, character.only = TRUE)
    }
  }
}
install_packages(required_packages)
```

### Running the Code

1. **Load the Data**: Adjust the `file_path` in the code to the location of your dataset.
2. **Run Time Series Analysis**: The script performs stationarity tests, fits ARIMA models, and selects the best one based on AIC/BIC.
3. **Forecast Future Values**: The best model is used to forecast future points, and the forecast is visualized alongside actual future values for comparison.

## Results

- The model with the lowest AIC/BIC is selected for forecasting. 
- The forecasted future values are plotted, and a residual analysis is performed to confirm model adequacy.


Feel free to explore the code, contribute, or raise issues in the repository if you encounter any problems.
