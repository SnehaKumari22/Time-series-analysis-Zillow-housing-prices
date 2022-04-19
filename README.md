# Time-series-analysis-Zillow-housing-prices
Forecasting the median sold price for housing data from Zillow.

The goal of this report is to research how we can forecast the median future sold price for housing in California based on time series models. We are using the Zillow dataset recorded Feb 2008- Dec 2015 monthly as our training set, including median sold price for housing in California, median mortgage rate, and unemployment rate, and trying to predict the Jan- Dec 2016 median sold price for housing in California.

### Overview of the report's content:

- Data Exploration
- Testing for stationarity
- Differencing and Decomposition
- Modelling
- - ARIMA Family
- - - ARIMA Models
- - - SARIMA Models
- - - SARIMAX Models
- - Holt Winters Exponential Smoothing
- - Prophet model
- Model Selection process
- Model estimation and validation
- Best Model
- Predictions
- Final Error Calculation
- Results

## Conclusion
We attempt to predict the Median Housing Prices for the near future using the history data and exogenous variables. From our initial exploratory analysis, we find that the time series data shows an obvious trend. Some seasonality can be seen towards the later half of the data.

For our analysis, we used a variety of candidate time series forecasting models ranging from ARIMA family to prophet. For initial univariate analysis, we start with low complexity models by just considering simple ARIMA models with only trend components and no seasonality. We selected the
best candidate models with and without seasonality using different information criteria. Comparing the one-step cross validation RMSE of each of these candidate models, we found that ARIMA(3,1,0)(1,0,1)[12] is our best model for the univariate ARIMA family.

Next, we performed a similar procedure for Exponential Smoothing models. We considered all the possible combinations for trend and seasonality and we found that the Exponential Smoothing model with Multiplicative trend and no seasonality gives the best cross validation RMSE. We did not get good cross-validation results for the Prophet model. This is expected since the Prophet model is not ideal for time series data with monthly frequency.

Next, we analysed SARIMA models with different combinations of exogenous variables. On comparing the cross-validation RMSE, we found that SARIMAX(2,0,0),(0,1,2)[12] with Unemployment rate as the exogenous variable gives the best results. 

Comparing the cross-validation RMSE values for our best models from different cases, we find that SARIMAX(2,0,0),(0,1,2)[12] has the lowest RMSE and hence we chose it as our best model. On the test data, we get a prediction RMSE value of 9596.31for our best model.

## Further Improvements
For SARIMA models with exogenous variables, the exogenous variables for the test set are generally unavailable in a real world setting. Hence, ideally we need to consider the prediction of the exogenous variables for the test set as a separate univariate time series analysis problem. Once we have the test predictions for exogenous variables, we can use those predictions in the SARIMAX model to predict the target time series variable.

Also, the auto-arima function uses an information criterion to find the best candidate model parameters. However, auto-arima doesn’t cover the entire parameter space and hence we may miss out on the best model. So, we can use a different model selection function like ”bic_sarima” which covers the entire parameter space. Using the current version of bic_sarima is not feasible because it runs very slow.

For better forecasting predictions with exogenous variables, we can also explore deep learning models like Recurrent Neural Networks (RNNs), Long Short-Term Memory (LSTM), and Gated Recurrent Unit (GRU).
