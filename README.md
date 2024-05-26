# Univariate Time-Series Forecast with Prophet Model

## Introduction
### What is Univariate?
Univariate is a term commonly used in statistics to describe a type of data that consists of observations on
only a single characteristic or attribute such as a time series data.
We can use stock prices as an example since the Closing price of tomorrow is independent and cannot be
predicted using other attributes like the day’s high and low since those attributes haven’t occurred yet or are
still unknown. That is why many of the prediction models of stock prices that can be found online are
misleading since they require other independent attributes to make predictions.
### What is Prophet?
Prophet is a procedure for forecasting time series data based on an additive model where non-linear trends are fit
with yearly, weekly, and daily seasonality, plus holiday effects.
Hence, we will be using univariate analysis and Facebook’s Prophet model to understand the characteristics
of the stock's price movements over a certain period.

## Data Exploration and Split

For this analysis, we are going to split
the data (Amazon Stock Price) into 3 parts.
Training, Validation, and Testing sets.
1. Training to fit the model
2. Validation to fine-tune model
parameters
3. Testing for our forecast
analysis

![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/32a764ee-ccae-4819-851e-3317dbf68c9a)

## Fit & Training Default Model
### Overfitting Avoidance
To avoid overfitting or leakage to the model, we created several time-series df with empty observations for the validation  and final testing forecast.

![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/988c7e63-6c17-4bc8-b909-eb18a48992de)

Default model without adjustments:
![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/54f3bcce-6677-4d1b-9c31-eb39a9fb9cce)

Here, we can see the model’s trend line on the training data set and its uncertainty interval.


## Identifying Changepoint & Seasonality

### Trend Changepoints & Scales
By default, Prophet will automatically detect these changepoints and will allow the trend to adapt appropriately.

If the trend changes are being overfit (too much flexibility) or underfit (not enough flexibility), you can adjust the strength of the sparse prior using the input argument changepoint_prior_scale.

By default, this parameter is set to 0.05. Increasing it will make the trend more flexible and vice versa.

We can visualize how different changepoint scales affect the model.

![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/5c5009c8-ed7f-4b2e-b8a8-92560915f936)
![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/5be76e14-79ee-43ef-9f88-589e6fa8aa46)
![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/37ca94d7-667e-45f6-a47f-7bd3f166728f)
![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/fac30020-875b-4cd7-98e5-4aa0c52dfea0)

### Seasonality
Seasonalities are estimated using a partial Fourier sum. There is a parameter seasonality_prior_scale which similarly adjusts the extent to which the seasonality model will fit the data.

The additive model is useful when the seasonal variation is relatively constant over time. The multiplicative model is useful when the seasonal variation increases over time.
Extra regressors are put in the linear component of the model, so the underlying model is that the time series depends on the extra regressor as either an additive or multiplicative factor

By default, this parameter is 10, which provides very little regularization. Reducing this parameter dampens holiday effects.

### Default Model
The default model’s forecast versus the Validation data set (Actual).

![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/ee678492-a54a-4930-b6c8-5df8ac89483e)

### Additive & Multiplicative:
The additive model is useful when the seasonal variation is relatively constant over time. 
The multiplicative model is useful when the seasonal variation increases over time.
These extra regressors are added in our cross-validation of the model to find if the model for this time series depends on the regressor as either an additive or multiplicative factor.


## Identifying Best Parameters with Cross Validation

Cross-validation is performed using 366 days of initial training with 90-day horizons on 45-day intervals.
![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/d2391138-47b8-47c9-99e4-14c20ff8ad2d)

### Best parameters for model
'changepoint_prior_scale': 0.5, 'seasonality_mode': 'multiplicative', 'seasonality_prior_scale': 0.01

## Forecast & Findings
### Final Model
![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/6d7bc3b7-7c14-4496-8a41-ccc6144772f3)
### Forecast Analysis
![image](https://github.com/FooZheShen/Univariate-Prophet-Stock-Forecast/assets/153910230/5dfe3527-beba-48b4-af3b-341fe91a0873)

### Final Thoughts

From the chart, the model can detect the trend movement of the stock price well within the confidence interval.
The forecast for the final prediction and actual stock price from November 2023 to today’s date, has a mean error of 7.60 USD. 

Overall, the model performed well in forecasting trend trajectory on a short-term horizon.











