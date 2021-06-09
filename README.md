# S&P500-forecast

## Project Overview

Repository for the S&P500 Forecast Project
- Developed a forecasting tool using Auto-ARIMA and FBProphet to forecast future closing prices of the S&P 500 
- Forecasting tool is trained from the past 5 years of closing prices.
- Auto-ARIMA model has a Mean Absolute Percentage Error of 0.004912, which means that the model predicted the correct prices 99.5% of the time when tested against the validation period.

## Codes and Resources Used

**Python Version:** 3.8

**Packages:** pandas, numpy, sklearn, matplotlip, seaborn, statsmodel, pmdarima, fbprophet, ipywidgets

**Web Framework Requirements**: ```pip install -r requirements.txt```

**Data Source:** https://finance.yahoo.com/quote/%5EGSPC/history?period1=1465344000&period2=1623110400&interval=1d&filter=history&frequency=1d&includeAdjustedClose=true
- https://www.machinelearningplus.com/time-series/time-series-analysis-python/
- https://www.kdnuggets.com/2020/01/stock-market-forecasting-time-series-analysis.html
- https://www.analyticsvidhya.com/blog/2018/09/non-stationary-time-series-python/
- https://github.com/amitrani6/time-series-examples
- https://facebook.github.io/prophet/docs/quick_start.html

## Data Preparation 

- Scraped the past 5 years of S&P 500 prices from Yahoo Finance and wrote to a CSV file
- Converted the String data to the appropriate types (date from dates and floats for numbers)

## Data Visualisation

- Plotted the prices and volume against date to observe for trends and seasonality. Obvious upward trend noticed.
- Plotted the closing prices against month for each year to check for annual seasonality. No obvious annual seasaonality observed.

## Stationarity

- Chose adjusted closing prices as the target variable for standardisation
- Plotted rolling mean and standard deviation to observe changes in these parameters over time. 
- Tested the stationarity of the time series using the Dickey-Fuller Test: p-value 0.947936 
- Since p-value > 0.05, we have insufficient evidence to reject the null hypothesis (Prices are thus not stationary)
- Since the data is not stationary, we can decompose it into its 4 constituents: observed, trend, seasonal and residual.
- We notice the presence of trend and seasonality in the pricing.
- The residual is confirmed to be stationary.
- To reduce the magnitude of the trend and deviations, we transform the prices with log.

## Auto-ARIMA

- Split data into training and validation sets (9:1) 
- Ran Auto-ARIMA to obtain the optimum ARIMA model for forecasting: ARIMA(3,1,2)
- Fitted the model and plotted the prediction against the test period.
- Obtained a Mean Absolute Percentage Error of 0.004912, which means that the model predicted the correct prices 99.5% of the time when tested against the validation period.


## Prophet

- Fitted a prophet model to predict 1 year of stock prices (until June 2022)
- Plotted interative widgets to visualise the prices

![Predictor Interface](https://github.com/edologgerbird/SP500-forecast/blob/main/assets/screenshot0.png "Predictor Interface")
![Predictor Interface](https://github.com/edologgerbird/SP500-forecast/blob/main/assets/screenshot1.png "Predictor Interface")