---
layout: base
title: An Introduction to Time series Forecasting
permalink: TimeSeriesFore.html
---

<h2> {{page.title}} </h2>

# Overview
Time series is *an ordered sequence of values of a variable at equally spaced time intervals.* These values are dependent on time and can be taken yearly, monthly, weekly, hourly, or even by the minute.

**Time series analysis** involves analysing time series data to extract meaningful statistics (pattern analysis) and other data characteristics (anomaly detection); it is a preparatory step to **Time series forecasting** - which uses a model to predict future values based on historically observed values. Typically, the first step in time series forecasting is to remove the effects of the trend or season that exist within the data to make it stationary.

Time series forecasting aims to isolate the pattern from the error by understanding the pattern’s level, trend, and seasonality. The error is then measured using statistical measurements to describe both how well a pattern reproduces historical values and to estimate how accurately it projects the values into the future.

The best way to approach time series forecasting is to try multiple modelling methods depending on the type of data you have, and then rank them according to which model has the lowest error.

Time series is different from regression analysis because of its time-dependent nature. 

# Time series Components

## Trend
The trend can be defined as the gradual upward, downward, or horizontal movement of values which are noted as the change in time. 

A trend can be analysed as local or global. Local trends are the values between time-series going in either an upward or downward direction, and the global trend is an overview of the whole time series. 

## Level                                                                                                                                      
The Level is the average value in the time series. 

## Seasonality
Seasonality is a characteristic of a time series in which the data experiences regular and predictable changes (periodic fluctuations) that are often observed within a year or less. Essentially, **a predictable pattern is observed in a regular interval of time**, sometimes also referred to as periodic time series. 

<figure>
  <img src="assets/img/TSF_1.png" width="400" height="200">
  <figcaption><b>Seasonal pattern illustrated on a quarterly basis</b></figcaption>
</figure>

The seasonal component of a time series can be removed via a statistical method called deseasonalisation or seasonal adjustment. 

### Type of seasonality
To select the appropriate model to produce forecasts, the type of seasonality needs to be known. Seasonality can appear in two forms: additive and multiplicative.
Seasonal variation is relatively constant over time in an additive time series, where the components **add** together to form the time series. 
In a multiplicative time series, the components **multiply** together to form the time series, and seasonal variations increase over time. 

### Identifying if a time series is additive or multiplicative
If the seasonality and residual components are **independent** of the trend, then it is an additive series. If the seasonality and residual components are in fact **dependent**, meaning they fluctuate on trend, then it is a multiplicative series.

Python code for analysing chart seasonality can be found [here](https://sigmundojr.medium.com/seasonality-in-python-additive-or-multiplicative-model-d4b9cf1f48a7).

<figure>
  <img src="assets/img/TSF_2.png" width="400" height="200">
  <figcaption><b>Additive vs Multiplicative time series</b></figcaption>
</figure>

## Cycles
A cycle, also referred to as a non-seasonal cycle, consists of patterns that are repetitive in the whole time series. In cyclic variations, **the peaks and troughs don’t occur in a regular interval of time**. 

<figure>
  <img src="assets/img/TSF_3.png" width="400" height="200">
  <figcaption><b>Graph illustrating a cyclic pattern</b></figcaption>
</figure>

## Pulses and Steps
Pulses - observations where any sudden movements in the values occur for a small/temporary amount of time.
Steps - observations where any sudden movements in the values occur for a large/permanent amount of time.

<figure>
  <img src="assets/img/TSF_4.png" width="400" height="200">
  <figcaption><b>A pulse can be observed in point 1/73 till 1/82, and after point 1/82, steps can be observed till the last point.</b></figcaption>
</figure>

## Outliers / Irregular fluctuations
Outliers and Irregular fluctuations (often called white noise) are variations that occur due to sudden causes and are unpredictable. If the time series data only has White Noise as a component, it cannot be used for prediction.

<figure>
  <img src="assets/img/TSF_5.png" width="400" height="600">
  <figcaption><b>Various types of outliers that can occur in any time series</b></figcaption>
</figure>

<figure>
  <img src="assets/img/TSF_6.png" width="400" height="200">
  <figcaption><b>Main time series components</b></figcaption>
</figure>
    
# When not to use time-series analysis and forecasting
1. When the values are **constant** as this indicates that the values are not dependent on time. 
2. When the values are in the form of a **function** e.g. sin x, cos x.
3. When a time-series only contains white noise as a component. 

# Importing & Cleaning Data
It’s important to Import necessary packages and libraries.

Data cleaning is then required to remove a range of data issues, these can include:
- Missing values
- Data redundancy 
- Data inconsistency (data types)
- Invalid values
- Outliers

# Exploratory Data Analysis

## Linear Regression
Linear regression can be used with time series to identify the overall trend. It is also known as Ordinary Least Squares (OLS) because it minimises the sum of the squared distances between the data points and the regression line

## Rolling Averages

### Simple Moving Average (SMA)
This is essentially an equally weighted mean of previous data. SMA uses a sliding window to take the average over a set number of time periods, it drops the oldest observation as new observations get added. 

### Cumulative Moving Average (CMA)
CMA considers all prior observations, it averages out all previous observations up until the current observation. It’s great for analysing trends and smoothing out the time series.

### Exponential Moving Average (EMA)
EMA gives more weight to the most recent observation, it’s a better way to capture the movement of the trend.

Python code on moving averages can be viewed [here](https://www.datacamp.com/community/tutorials/moving-averages-in-pandas).

## Polyfit
Polyfit can be used to create a line of best fit through the data by calculating the coefficients of any polynomial function for a set time series. 

<figure>
  <img src="assets/img/TSF_7.png" width="200" height="200">
  <figcaption><b>Line of best fit created using Polyfit</b></figcaption>
</figure>

# Time Series Decomposition
Decomposition is often done to help improve understanding of the time series, but it can also be used to improve forecast accuracy.

Decomposition splits the time-series into trend, seasonal, and residual components, these can then be studied individually in isolation. 
The charts below illustrate time-serie decomposition; trend and seasonality can be understood more precisely using this. 

<figure>
  <img src="assets/img/TSF_8.png" width="400" height="600">
  <figcaption><b>Time-series decomposition</b></figcaption>
</figure>

<figure>
  <img src="assets/img/TSF_9.png" width="400" height="400">
  <figcaption><b>Time-series decomposition</b></figcaption>
</figure>

Other types of time series decomposition include the following:
- Classical decomposition
- X11 decomposition
- SEATS decomposition
- STL decomposition

Detailed information on the above can be found [here](https://otexts.com/fpp2/decomposition.html). 

# Stationarity and Differencing

## What is Stationarity?
In stationary time series, the mean, variance, and standard deviation of the observed value over time are almost constant whereas in non-stationary time series this is not the case. Non-stationary time series contain additional patterns, like Trends, Seasonality, or Cycles.

## How do we check for stationarity?
The following tests can be conducted to check for stationarity:

### Unit Root Tests such as Dickey-Fuller Test, Augmented Dickey-Fuller (ADF) Test, and the KPSS Test.
Unit root is a characteristic of a time series that makes it non-stationary. 
The DF and ADF test checks whether the series has a unit root or not. If it exists, the series has a linear trend. However, if it’s not, we can say that the model is stationary.
The number of unit roots contained in the series corresponds to the number of differencing operations required to make the series stationary.

### Unit route KPSS Test
The KPSS tests for stationarity of the series around a ‘deterministic trend’. This implies that the slope of the trend in the series does not change permanently. That is, even if the series goes through a shock, it tends to regain its original path.

### Lungebox Test 
A Lungebox Test takes out seasonality/trend from data
The p-value should not pass the blue in a Lungebox Test, if it does, then the model does not meet the requirements for conducting a forecast.

### Autocorrelation Function (ACF)
The ACF plot, also known as the autocorrelation plot, is useful for identifying non-stationary time series. The autocorrelation indicates dependencies of value at the current time step on the previous time steps. Essentially, the plot is used to see the correlation between the points, up to and including the lag unit.
For a stationary time series, the ACF will **drop to zero** relatively **quickly**, while the ACF of non-stationary data **decreases slowly**. Also, for non-stationary data, the value of  
**r↿** is **often large and positive**.

### Partial Auto-correlation Function (PACF)
The PACF measures the correlation between the current variable and the lagged variable after eliminating the correlation from previous lags. In simple terms, the PACF removes the lags that cause autocorrelation.

## Differencing and the Danger of Over-differencing
- We can make a non-stationary time series stationary by differencing consecutive observations.
- Differencing cannot remove heteroskedasticity - this is when the variance of the series changes over time. 
- The most common cause of H is when fluctuations are as a percentage of the value of the time series, not a fixed number; the variance in a time series is proportional instead of absolute. 
- If your time series is heteroskedastic, you will need to transform it before modelling it with SARIMAX.

# Train-test Split
- Before building a model, data should be train-test split. 
- Splitting data into a training and test set, prevents the model from overfitting. 
- Typically 70-80% of data is a good size for a training set. It’s best to take the first part of the data set as training, and the last part for testing, not a random split as in a regression or classification model.
- Never conduct a train-test split near a sudden large change in the data.

Best practice and python code can be viewed [here](https://www.watchful.io/resources/what-should-my-train-test-split-be).

<figure>
  <img src="assets/img/TSF_10.png" width="400" height="200">
  <figcaption><b>Train-test Spilt</b></figcaption>
</figure>

<figure>
  <img src="assets/img/TSF_11.png" width="200" height="200">
  <figcaption><b>Machine Learning aspect of the split
</b></figcaption>
</figure>

# Creating a Model / Modelling Methods ([add in](https://docs.google.com/document/d/13S13vx3NYa23iVDofk1HSKXV5MPC_kZTBkeR1HIwCNo/edit)) 

## Simple Forecasting

### Naïve approach
The Naïve approach is the simplest forecasting method where the most recent observation or value is used to set all forecasts. 
The naive method isn’t suited for datasets with high variability. It is best suited for stable datasets.

### Seasonal Naïve
For seasonal data, a related idea is to use the corresponding season from the last year of data. For example, if you want to forecast the sales volume for next March, you would use the sales volume from the previous March. This is implemented in the snaive() function, meaning, seasonal naive.

Sometimes one of these simple methods will be the best forecasting method available; but in many cases, these methods will serve as benchmarks rather than the method of choice.

## Classic Non-Seasonal Forecasting
The following methods attempt to forecast by removing extreme changes in past data where repeating cycles of data values are not present. 

### Single Moving Average (SMA) 
This method smooths historical data by averaging the last several periods and projecting the last average value forward.

This method is best for volatile data with no trend or seasonality. It results in a straight, flat-line forecast.

<figure>
  <img src="assets/img/TSF_12.png" width="400" height="200">
</figure>

### Double Moving Average (DMA)
This method applies the moving average method twice, once to the original data and then to the resulting single moving average data. The method then uses both sets of smoothed data to project forward.

This method is best for historical data with a trend but no seasonality. It results in a straight, sloped-line forecast.

<figure>
  <img src="assets/img/TSF_13.png" width="400" height="200">
</figure>

**Parameters** in SMA & DMA are known as periods. For SMA, the periods can be a whole number between 1 and half the number of data points. For DMA, the periods can be any whole number between 2 and one-third of the number of data points.
### Single Exponential Smoothing (SES) 
SES weights all of the past data with exponentially decreasing weights going into the past ( more recent data has greater weight). Weighting in this way largely overcomes the limitations of the moving averages technique. 

This method, which results in a straight, flat-line forecast is best for volatile data with no trend or seasonality.

<figure>
  <img src="assets/img/TSF_14.png" width="400" height="200">
</figure>

### Double Exponential Smoothing (DES)
DES applies SES twice, once to the original data and then to the resulting SES data.

This method is best for data with a trend but no seasonality. It results in a straight, sloped-line forecast.

<figure>
  <img src="assets/img/TSF_15.png" width="400" height="200">
</figure>

**Parameters** in SES and DES differ. SES contains only one parameter: Alpha (α) - this is the smoothing constant. 
DES contains two parameters: Alpha (α), the same smoothing constant as in SES, and Beta (β) - also a smoothing constant but is used during second smoothing.
The **value** of α and β can be any number **between 0 and 1**, not inclusive.

## Classic Seasonal Forecasting
Seasonal forecasting methods extend the non-seasonal forecasting methods by adding an additional component to capture the **seasonal** behaviour of the data.

### Seasonal Additive 
This method calculates a seasonal index for historical data that does not have a trend. The method produces exponentially smoothed values for the level of the forecast and the seasonal adjustment to the forecast. The seasonal adjustment added to the forecasted level produces the seasonal additive forecast.

This method is best for data **without trend** but with seasonality that **does not** increase over time. It results in a curved forecast that **reproduces** the seasonal changes in the data.

<figure>
  <img src="assets/img/TSF_16.png" width="400" height="200">
</figure>

### Seasonal Multiplicative 
This method calculates a seasonal index for historical data that does not have a trend. The method produces exponentially smoothed values for the level of the forecast and the seasonal adjustment to the forecast. The seasonal adjustment is multiplied by the forecasted level, producing the seasonal multiplicative forecast.

This method is best for data **without trend** but with seasonality that **increases** or **decreases** over time. It results in a curved forecast that **reproduces** the seasonal changes in the data.

<figure>
  <img src="assets/img/TSF_17.png" width="400" height="200">
</figure>

### Holt-Winters Exponential Smoothing
Python code can be found [here](https://medium.com/analytics-vidhya/python-code-on-holt-winters-forecasting-3843808a9873).
 
Similar to SES and DES, the Holt-Winters Exponential Smoothing works to assign exponentially decreasing weights, giving more importance to more recent values so, when we move back in time, we would see diminishing weights. There are two parts to this method which are discussed below. 
Holt-Winters’ Additive 
This method produces exponentially smoothed values for the level of the forecast, the trend of the forecast, and the seasonal adjustment to the forecast.

This method is best for data with trend and seasonality that **does not** increase over time. It results in a curved forecast that shows the seasonal changes in the data.

<figure>
  <img src="assets/img/TSF_18.png" width="400" height="200">
</figure>

Holt-Winters’ Multiplicative 
This method also calculates exponentially smoothed values for level, trend, and seasonal adjustment to the forecast. The seasonal multiplicative method multiplies the trended forecast by the seasonality.

This method is best for data with trend and with seasonality that **increases** over time. It results in a curved forecast that **reproduces** the seasonal changes in the data.

Three smoothing **parameters** are used in the above four seasonal forecasting methods:

alpha (α) — Smoothing parameter for the level component of the forecast. 
beta (β) — Smoothing parameter for the trend component of the forecast.
gamma (γ) — Smoothing parameter for the seasonality component of the forecast. 

The **value** of these parameters can be any number **between 0 and 1**, not inclusive.

[Best practice](https://www.statsmodels.org/dev/examples/notebooks/generated/ets.html) for exponential smoothing
## ARIMA and SARIMA
The acronym ARIMA stands for AutoRegressive (AR) Integrated (I) Moving Average (MA). This statistical analysis model uses time-series data to predict future trends. 

ARIMA has three trend parameters; **p**, **d**, and **q**.

- **AR = p** – p is the number of autoregressive terms (AR part). It allows us to incorporate the effect of past values into our model. Intuitively, this would be similar to stating that it is likely to be warm tomorrow if it has been warm the past 3 days. P is often referred to as the lag order as it’s the number of lag observations. 

- **I = d** – d is the number of times that the raw data is differenced in order to achieve stationarity. Intuitively, this would be similar to stating that it is likely to be the same temperature tomorrow if the difference in temperature in the last three days has been very small. D is also known as the degree of differencing.

- **MA = q** – q is the number of lagged forecast errors in the prediction equation (MA part). This allows us to set the error of our model as a linear combination of the error values observed at previous time points in the past. Q is also known as the order of the moving average.

SARIMA is a seasonal equivalent model like ARIMA. It is used on datasets that have seasonal cycles. The parameters in a SARIMA model include the trend parameters, **p**, **d**, and **q** (like in ARIMA) but also include the seasonal parameters, **P**, **D**, **Q**, and **m/s**. 

- **P** = Seasonal autoregressive order.
- **D** = Seasonal difference order.
- **Q** = Seasonal moving average order.
- **m/s** = The number of time steps for a single seasonal period.

### Hyperparameter Optimisation for Model Selection
- This is also referred to as a **grid search** to iteratively explore different combinations of parameters
- This is used in ARIMA to determine the ARIMA(p,d,q)(P,D,Q) values.  

## Using Prophet 
Prophet is a procedure for forecasting time series data based on an **additive model** where non-linear trends are fit with yearly, weekly, and daily seasonality, plus holiday effects; it automatically includes error terms.

The input to Prophet is a dataframe with two columns: **ds** and **y**. The **ds** column should be in a timestamp format and the **y** column in a numeric format. 

It works best with time series that have **strong seasonal effects** and several seasons of historical data. Prophet is robust to missing data and shifts in the trend, and typically handles outliers well.

## Advanced Forecasting
Advanced techniques like BATS and TBATS are designed to handle time series that contains multiple seasonality.

### BATS
Exponential smoothing state-space model with Box-Cox transformation, ARMA errors, Trend and Seasonal components
- [BATS R Code](https://github.com/robjhyndman/forecast/blob/master/R/forecastBATS.R)

### TBATS
Trigonometric Exponential smoothing state-space model with Box-Cox transformation, ARMA errors, Trend and Seasonal components
- [TBATS R Code](https://github.com/robjhyndman/forecast/blob/master/R/forecastTBATS.R)
- [TBATS & BATS Python Code](https://pypi.org/project/tbats/)

# Model Performance Measures
The following performance measures provide a summary of how ‘good’ the forecasting model is. **Theil’s U**, and **Durbin-Watson** are also amongst other measures that are used. 

The python code for most of the measures below can be found on the [machine learning mastery website](https://machinelearningmastery.com/time-series-forecasting-performance-measures-with-python/) and this [blog](https://grisha.org/blog/2016/01/29/triple-exponential-smoothing-forecasting/).
Guidance on choosing the right measure can be found [here](https://towardsdatascience.com/forecast-kpi-rmse-mae-mape-bias-cdc5703d242d).
The measures in bold are the most widely used.

## AIC / BIC Value 
- These are known methods of scoring and selecting a model. 
- The Akaike's Information Criteria (AIC) measures how well a model fits the data.
- A model that fits the data very well while using lots of features will be assigned a larger AIC score than a model that uses fewer features to achieve the same goodness-of-fit. 
- The Bayesian Information Criteria (BIC), also known as the Schwarz Criterion, is another index measure used for scoring and selecting a model. It estimates the likelihood of a model to predict.
- The best model for the data will be the one with the lowest AIC / BIC values. 

## (Residual) Forecast Error
- This is calculated as the expected value minus the predicted value.
- A forecast error of zero indicates no error or perfect skill for that forecast.

## Forecast Bias (Mean Forecast Error)
- This is calculated as the average of the forecast error values.
- Forecast errors can be positive and negative. This means that when the average of these values is calculated, an ideal mean forecast error would be zero.
- A forecast bias of zero, or a very small number near zero, shows an unbiased model.

## Mean Absolute Deviation (MAD) 
- MAD (mean absolute deviation) is an absolute error measure, which is the difference between the expected and actual values. 
- Although MAD is still fairly reliable and widely used, it is most accurate for **normally distributed** data.

## Mean Absolute Percentage Error (MAPE) 
- MAPE is a relative error measure that uses absolute values. 
- MAPE has two advantages. First, the absolute values keep the positive and negative errors from cancelling out each other. Second, because relative errors do not depend on the scale of the dependent variable, MAPE lets you compare forecast accuracy between **differently scaled** time-series data.
- Generally, an MAPE < 10% is considered excellent, MAPE < 20% is considered good.

## Mean Square Error (MSE)
- MSE is an absolute error measure that calculates the average of the squared forecast error values. Squaring the forecast error values forces them to be positive; it also puts more weight on large errors.
- The score gives worse performance to models that make large wrong forecasts
- The error values are in squared units of the predicted values.
- An MSE of zero indicates perfect skill or no error.

## Root Mean Squared Error (RMSE) 
- RMSE is the MSE that has been transformed back into the original units of the predictions by taking the square root of the mean squared error score to keep the positive and negative deviations from cancelling out one another.
- RMSE tends to exaggerate large errors, which can help eliminate methods with large errors.
- An RMSE of zero indicates no error.

# Additional Notes on Modelling Methods and Techniques

- [Oracle’s Crystal Ball’s Documentation](https://docs.oracle.com/cd/E57185_01/CBREG/ch06s02s01.html) explains the scientific approaches to forecasting usually fall into one of several categories:
  - **Time-series** — Performs time-series analysis on past patterns of data to forecast results. This works best for stable situations in which conditions are expected to remain the same.
  - **Regression** — Forecasts results using past relationships between a variable of interest and several other variables that may influence it. This works best for situations in which you need to identify the different effects of different variables. This category includes multiple linear regression.
  - **Simulation** — Randomly generates many scenarios for a model to forecast the possible outcomes. This method works best where you may not have historical data, but you can build the model of the situation to analyze its behaviour.
  - **Qualitative** — Uses subjective judgement and expert opinion to forecast results. These methods work best for situations for which no historical data or models are available.
- Exponential smoothing and ARIMA models are the two most widely used approaches to time series forecasting. Exponential smoothing models are based on a description of the trend and seasonality in the data, and ARIMA models aim to describe the autocorrelations in the data.
- Sometimes it becomes difficult to model time series which have non-seasonal cyclical patterns because the presence of non-seasonal cycles generally **increases uncertainty** in forecasting. When modelling such a time series it is necessary to consider the non-seasonal cycle to take into account. In many cases, it is suggested to use the [LSTM models](https://en.wikipedia.org/wiki/Long_short-term_memory) for fitting and modelling such time series because they facilitate us to minimize uncertainty in forecasting.
- It’s important to understand that forecasting models can outperform one another of different datasets. Therefore, it doesn’t mean that one model that performs best on one type of dataset will perform the same for all others.
- To achieve a better model, tune the parameters.
- Mathematical formulas for models can be found [here](https://people.bath.ac.uk/zt354/SLS_Resources/Matt_Nunes_TimeSeries.pdf).
- According to [Hamjah](https://core.ac.uk/download/pdf/214006095.pdf) (2014: 170-171), the following steps are worth considering when auctioning the Box and Jenkins approach to **ARIMA** forecasting: 
  - Preliminary analysis: Data at hand should conform to a stationary stochastic process. 
  - Identification: specify the orders p, d, q of the ARIMA model so that it is clear the number of parameters to estimate and also recognition of the importance of autocorrelation functions in the model. 
  - Estimate: efficient, consistent, sufficient estimate of the parameters of the ARIMA	model (maximum likelihood estimator). 
  - Diagnostics: Model to be checked for appropriateness using tests on the parameters and residuals of the model. Even when the model is rejected, still this is a very useful step to obtain information to improve the model. 
  - Usage of the model: Once test outcomes are sufficiently passed or satisfies the specification, it can then be used to interpret a phenomenon based on forecast outcome(s). 
- Additional Notebooks and Tutorials relating to time series analysis in python can be found on [Kaggle](https://www.kaggle.com/getting-started/54280). 

# Guided Code Implementation (Add in A&E forecast)
Using public A&E Attendance data
[Linear Regression](https://colab.research.google.com/drive/1OVaCgAVNmWCWlopenOvjz8uijw8eWyMd?pli=1#scrollTo=Em363cpxHncN) A&E
ARIMA A&E
[Prophet](https://github.com/nhs-pycom/coding-club-prophet) + Prophet A&E

References
1. [Rules for identifying ARIMA Models](https://people.duke.edu/~rnau/arimrule.htm)
2. [https://machinelearningmastery.com/exponential-smoothing-for-time-series-forecasting-in-python/](https://machinelearningmastery.com/
exponential-smoothing-for-time-series-forecasting-in-python/)
3. [https://kourentzes.com/forecasting/2014/11/09/additive-and-multiplicative-seasonality/](https://kourentzes.com/forecasting/2014/11/09/additive-and-multiplicative-seasonality/)
4. [https://docs.oracle.com/cd/E40248_01/epm.1112/cb_statistical/frameset.htm?ch07s02s03s04.html](https://docs.oracle.com/cd/E40248_01/epm.1112/cb_statistical/frameset.htm?ch07s02s03s04.html)
5. [Complex seasonal forecasting](https://pdf.sciencedirectassets.com/280203/1-s2.0-S1877050918X00088/1-s2.0-S1877050918308688/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEAMaCXVzLWVhc3QtMSJHMEUCIGptsZAPTHCZNrngV68mSiiGIMayKM9be7qffjTOUBbSAiEAqHVjk5Gh3nYGNMFJor0v%2FQTLkYaYMxmqGisW%2F4ssayQqgwQIrP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FARAEGgwwNTkwMDM1NDY4NjUiDN0uP6%2Fey8KRmdvNeyrXAyvoFVX49m9QZtR2c0BXDn2YssjnP87FvFQx6%2F5x%2F6dX1h%2BJNMgveUR%2BxCcQiSbVZTH2gQSMsQcKgntuuXwCvKZaMQ75c5tX%2B18DzE0c%2ByS1YNXr1vjrWiwRjb22s5hnyXS%2BTtayrUU1dlaSmm10bIQR46Mn%2BKLOlAZ48qD9oiuVi8C5Wna6ucQmBcwur2XYQJCpddMsSKLF4pVTtRI4N8IXvbaTh0s1S5wOW%2Fp2COiA%2F6sRI8mcTfXlcer51tZq%2Bj0P09%2F0tEoVEMq7KaIRYGjxo1VL1yt9m3lntF4fRWAwMug4JYmT8LBH9QV4E3MlfQZvozv0Ynelcpxzpf5yrQLDfro%2F5g6TKhQ2kgqHgpxZXjuS%2BKErMtSHd4VcrwY9%2FdsxfwDm%2B6umMKYOMs4YqMvoSpLu%2FRALVfD9sqfRMzvZG5sodvTF9AKcq1FFLk0pQpHdQrPU9NORvsr7Zv5XvjMnHClJ9yMqQ464n%2Bo%2B3wfHETssdCs4G0MCeJSbUM0b2%2B15E29TOnoFP1Wpv%2FTZl8oebM1AG%2BVViFbVBHO3LNosKNh1%2FK6wdxWAsU3OMgk2qF%2B9qEd%2B%2BlxhQ8TrihO1F3H5A475Sb5OaxFBRBdTus952iEmpTIIszDVv6CMBjqlAdcs%2Fmw%2FL3nMLUnIhF65VQ8rf1%2B3T7tfKEfWw6XFeO0qHp3GMmnVkmEEicNe8tUrrLwr%2FTosFG8fveI%2Fu11pPsju1CUVtUU3Xj8gcDRPcz8wBeEre60%2F7lkOYhQpSEfKO%2BfY9pd%2Bk7yM6yzO7sXJfOrQctVEWDGJazcmovtwVCgwMEoGnjyrKGlUspg%2BaPjBSWSwZiYqwq9g2b1QNGTA5a98YrS57A%3D%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20211107T195927Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTY3C4U6SRW%2F20211107%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=6a72181248cb6f3cde131d09ae562ce7479c7e6ee591edc6e3ad94b1df2f3615&hash=262200a57052435bb073e043fdc0c184e6acbeba17093da8b2f877e3a9ac8f10&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=S1877050918308688&tid=spdf-27d6aef1-fd45-44b0-995f-1a65894041af&sid=1682877b8e7b674ab88b28a8d6c71a7cd3d9gxrqb&type=client)
6. [https://medium.com/analytics-vidhya/holt-winters-forecasting-13c2e60d983f](https://medium.com/analytics-vidhya/holt-winters-forecasting-13c2e60d983f)
7. [https://medium.com/analytics-vidhya/python-code-on-holt-winters-forecasting-3843808a9873](https://medium.com/analytics-vidhya/
python-code-on-holt-winters-forecasting-3843808a9873)
8. [https://core.ac.uk/download/pdf/214006095.pdf](https://core.ac.uk/download/pdf/214006095.pdf) -  Comparison between Static and Dynamic Forecast in Autoregressive Integrated Moving Average for Seasonally Adjusted Headline Consumer Price Index
9. [https://medium.com/@analyttica/what-is-bayesian-information-criterion-bic-b3396a894be6](https://medium.com/@analyttica/what-is-bayesian-information-criterion-bic-b3396a894be6)
10. [https://community.jmp.com/t5/Short-Videos/What-is-BIC-how-do-you-use-it-and-what-is-a-good-BIC-value/ta-p/194416](https://community.jmp.com/t5/Short-Videos/What-is-BIC-how-do-you-use-it-and-what-is-a-good-BIC-value/ta-p/194416)
11. [https://www.avercast.com/post/naive-forecasting](https://www.avercast.com/post/naive-forecasting)
12. [https://otexts.com/fpp2/simple-methods.html](​​https://otexts.com/fpp2/simple-methods.html)
13. [https://www.analyticsvidhya.com/blog/2018/02/time-series-forecasting-methods/](https://www.analyticsvidhya.com/blog/2018/02/time-series-forecasting-methods/)
14. [https://towardsdatascience.com/how-to-detect-random-walk-and-white-noise-in-time-series-forecasting-bdb5bbd4ef81](https://towardsdatascience.com/how-to-detect-random-walk-and-white-noise-in-time-series-forecasting-bdb5bbd4ef81)
15. [https://people.duke.edu/~rnau/411rand.htm](https://people.duke.edu/~rnau/411rand.htm)
16. [https://machinelearningmastery.com/gentle-introduction-random-walk-times-series-forecasting-python/](https://machinelearningmastery.com/gentle-introduction-random-walk-times-series-forecasting-python/)
17. [https://towardsdatascience.com/how-to-model-time-series-data-with-linear-regression-cd94d1d901c0](https://towardsdatascience.com/how-to-model-time-series-data-with-linear-regression-cd94d1d901c0)
18. [https://rstudio-pubs-static.s3.amazonaws.com/487377_18327e7d7e87412282b92d870de14de0.html](https://rstudio-pubs-static.s3.amazonaws.com/487377_18327e7d7e87412282b92d870de14de0.html)
19. [https://towardsdatascience.com/limitations-of-arima-dealing-with-outliers-30cc0c6ddf33](https://towardsdatascience.com/limitations-of-arima-dealing-with-outliers-30cc0c6ddf33)
20. [https://towardsdatascience.com/q-q-plots-explained-5aa8495426c0#:~:text=Q%2DQ%20plots%20are%20used%20to,by%20looking%20at%20the%20plot](https://towardsdatascience.com/q-q-plots-explained-5aa8495426c0#:~:text=Q%2DQ%20plots%20are%20used%20to,by%20looking%20at%20the%20plot)
21. [https://towardsdatascience.com/an-end-to-end-project-on-time-series-analysis-and-forecasting-with-python-4835e6bf050b](https://towardsdatascience.com/an-end-to-end-project-on-time-series-analysis-and-forecasting-with-python-4835e6bf050b)
22. [https://towardsdatascience.com/statistical-test-for-time-series-a57d9155d09b](https://towardsdatascience.com/statistical-test-for-time-series-a57d9155d09b)
23. [https://www.itl.nist.gov/div898/handbook/pmc/section4/pmc4.htm](https://www.itl.nist.gov/div898/handbook/pmc/section4/pmc4.htm)
24. [https://towardsdatascience.com/introduction-to-time-series-forecasting-part-1-average-and-smoothing-models-a739d832315](https://towardsdatascience.com/introduction-to-time-series-forecasting-part-1-average-and-smoothing-models-a739d832315)
25. [https://www.machinelearningplus.com/time-series/augmented-dickey-fuller-test/](https://www.machinelearningplus.com/time-series/augmented-dickey-fuller-test/)
26. [https://www.machinelearningplus.com/time-series/kpss-test-for-stationarity/](https://www.machinelearningplus.com/time-series/kpss-test-for-stationarity/)
27. [https://towardsdatascience.com/6-amateur-mistakes-ive-made-working-with-train-test-splits-916fabb421bb](https://towardsdatascience.com/6-amateur-mistakes-ive-made-working-with-train-test-splits-916fabb421bb)
28. [https://medium.com/@rinu.gour123/train-and-test-set-in-python-machine-learning-how-to-split-58029a0d657b](https://medium.com/@rinu.gour123/train-and-test-set-in-python-machine-learning-how-to-split-58029a0d657b)
