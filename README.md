# Time-Series Analysis Using Auto ARIMA
Conducting a Univariate Time-Series analysis to forecast the number of airline passengers (from [Kaggle](https://www.kaggle.com/rakannimer/air-passengers)) and discuss through the traditional ARIMA implementation versus the more efficient, auto_arima way. All code can be found in [Time_Series.ipynb](https://github.com/mkosaka1/AirPassengers_TimeSeries) and all images can be found in the [Images](https://github.com/mkosaka1/AirPassengers_TimeSeries/tree/master/Images) folder.

## What is Time-Series Analysis?
One of the key concepts in data science is time-series analysis which involves the process of using a statistical model to predict future values of a time series (i.e. financial prices, weather, COVID-19 positive cases/deaths) based on past results. Some components that might be seen in a time-series analysis are:

- Trend : Shows a general direction of time series data over a period of time — trends can be increasing (upward), decreasing (downward), or horizontal (stationary).
- Seasonality : This component exhibits a trend that repeats with respect to timing, magnitude, and direction — such as the increase in ice cream sales during the summer months or increase in subway riders during colder months.
- Cyclical Component : A trend that has no set repetition over a certain time period. A cycle can be a period of ups and downs, mostly seen in business cycles — cycles do not exhibit a seasonality trend.
- Irregular Variation : Fluctuations in time-series data that is erratic, unpredictable and may/may not be random.
When conducting time-series analysis, there are either Univariate Time-Series analysis or Multivariate Time-Series analysis. Univariate is utilized when only one variable is being observed against time, whereas Multivariate is utilized if there are two or more variables being observed against time.
## What is ARIMA? Why Use Pmdarima?
ARIMA is an acronym which stands for Auto Regressive Integrated Moving Average and is a way of modeling time-series data for forecasting and is specified by three order parameters (p,d,q):
- AR(p): pattern of growth/decline in the data is accounted for
- I (d): rate of change of the growth/decline is accounted for
- MA (q): noise between time points is accounted for
There are three types of ARIMA models, ARIMA, SARIMA, and SARIMAX which differ depending on seasonality and/or use of exogenous variables.
Pmdarima‘s auto_arima function is extremely useful when building an ARIMA model as it helps us identify the most optimal p,d,q parameters and return a fitted ARIMA model.

**The general steps to implement an ARIMA model:**
1) Load and prepare data
2) Check for stationarity (make data stationary if necessary) and determine d value
3) Create ACF and PACF plots to determine p and q values
4) Fit ARIMA model
5) Predict values on test set
6) Calculate r²

## Traditional Implementation of an ARIMA Model
Determining *p,d,q* values by conducting a Dickey-Fuller test, and using ACF/PACF plots resulted in a r^2 value of -1.52. These results indicate that our model does not follow the trend of the data very well.

<p align="center">
  <img width="460" height="300" src="https://github.com/mkosaka1/AirPassengers_TimeSeries/blob/master/Images/FirstPredictions.jpg">
</p>

## Using pmdarima for Auto ARIMA model
In the previous method, checking for stationarity, making data stationary if necessary, and determining the values of p and q using the ACF/PACF plots can be time-consuming and less efficient. Using pmdarima’s auto_arima() function makes this task easier for us by eliminating steps 2 and 3 for implementing an ARIMA model. Let’s try it with the current dataset.

```
 model=auto_arima(train,start_p=0,d=1,start_q=0,
          max_p=5,max_d=5,max_q=5, start_P=0,
          D=1, start_Q=0, max_P=5,max_D=5,
          max_Q=5, m=12, seasonal=True,
          error_action='warn',trace=True,
          supress_warnings=True,stepwise=True,
          random_state=20,n_fits=50)
 ```
       
Using the trained model to forecast the number of airline passengers on the test set resulted in a r^2 value of 0.65 -- this model did a much better job at capturing the trend in the data compared to my first implementation of the ARIMA model.


<p align="center">
  <img width="460" height="300" src="https://github.com/mkosaka1/AirPassengers_TimeSeries/blob/master/Images/SecondPrection.jpg">
</p>


## Summary

Here we demonstrated the traditional implementation of an ARIMA model compared to the Auto ARIMA model using auto_arima(). While the traditional ARIMA implementation requires one to perform differencing and plotting ACF and PACF plots, the Auto ARIMA model using pmdarima’s auto_arima() function is more efficient in determining the optimal p,d,q values.

