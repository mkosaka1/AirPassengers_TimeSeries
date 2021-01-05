# Time-Series Analysis Using Auto ARIMA

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
