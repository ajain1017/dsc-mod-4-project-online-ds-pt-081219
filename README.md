
# NYC Housing Data Time Series Modeling

(technical presentation can be found in index.ipynb file)

## Goal

In this notebook, we perform time series analysis and SARIMA modeling to predict 5 best real estate investments (by zipcode) in NYC. Our investor in mind is risk averse; therefore, they are looking to minimize error and limit conifidence interval to provide the most confident zipcode investment suggestion. We are forecasting for a 2 year and 5 year investment.

## Data Exploration

![2-Year ROI](/images/twoyear.png)

![5-Year ROI](/images/fiveyear.png)

![10-Year ROI](/images/tenyear.png)

Our 2-year investment show a big gap between Manhattan and Brooklyn and the other three as well as a difference in the direction in which their return is going. As for our 5-year investment, all boroughs end around the same percentage. Our 10-year investment shows an upward trend for SI, Queens and the Bronx, whereas once again, Manhattan and Brooklyn are decreasing.  

The spike and decline due to new zipcodes in 2004 will influence our model, as well as the housing market crash; therefore, we will only work with data from 04/01/2008 till 04/01/2018, so we may have a 10-year dataset.

## Times Series Analysis

![Rolling Statistics](/images/rolling.png)

![Time Decomposition](/images/decomp.png)

Our rolling mean for all the zipcodes increased over time and was not stationary. Our Dickey-Fuller test confirmed this for all our zipcodes, except one, as we could not reject our null-hypothesis that the data is non-stationary. From decomposition, we see each zipcode experience an upward trend and seasonal change. As the seasonal change varies, we will use a SARIMA modeling and use auto_arima to find unique orders for each zipcode.

## SARIMAX Modeling

Instead of modeling for home value, we modeled and forecast the historical return on investment for 2-years and 5-years instead. This is because, there are way more factors that influence home value and overtime, return on investment over a period of time limit the influence of those factors.
We keep our last forecasted value, RMSE and a variability metric for that forecast as well. Since our investor is risk averse, I wanted to make sure we choose the forecasts that are the best predicted. Therefore, by taking the quotient of size of confidence interval over highest value of in the interval, we can see the significance of the size of confidence interval given the forecasted value obtained.

Our code involved a four step process of finding number of differences and seasonal differences, finding order using those number of differences, fitting the model and then forecasting our return on investment.

## Interpreting Results

![2-Year Forecast Results](/images/finalresults1.png)

![5-Year Forecast Results](/images/finalresults2.png)

Our 5 best zipcodes for 2-year investment are:  
10456 - Bronx, NY  
10305 - Richmond County, Staten Island, NY  
10304 - Richmond County, Staten Island, NY  
10307 - Richmond County, Staten Island, NY  
10314 - Richmond County, Staten Island, NY  

Our 5 best zipcodes for 5-year investment are:
10303 - Richmond County, Staten Island, NY  
11364 - Oakland Gardens, Queens, NY  
11358 - Murray Hill/Flushing, Queens, NY  
10309 - Richmond County, Staten Island, NY  
10305 - Richmond County, Staten Island, NY  

Looking at other information online, while sales dropped in the other boroughs during the second quarter of 2018, Staten Island saw an increase of 16 percent in the same period. The real estate market in Staten Island has been on the rise recently. Although the home values in Staten Island still similar to Queens, less expensive than almost all of the other boroughs. The new federal tax bill in NYC has also favored Staten Island housing, opening up opportunities for buyers. In a study by a home ownership investment firm, it is said that an individual must make around 400,000 annually to own Manhattan real estate and around 250,000 for Brooklyn owners. Therefore, as the rest of NYC moves out of the middle class, Staten Island offers attractive housing and thus makes a strong investment opportunity for 2-year and 5-year investments.

As for Queens, we see many families and young adults are looking to Queens as an alternative to Manhattan and Brooklyn as it offers cheaper housing while being very well connected to the rest of NYC through public transportation. There are great schools and an ethnically-diverse community in Queens, especially in the Flushing/Murray Hill/Oakland Gardens area, being the melting pot of Queens.

The 10467 zipcode in the Bronx is right next to Yankee stadium, as well as right on the border of Manhattan. This is similar to the Queens option for most buyers as you are very connected to Manhattan while not paying the very high price as in Manhattan.

## Future Work

− Keep in mind, our forecasts were solely based on past monthly home values. I would look to add more features to better predict housing prices in the future  
− I would look to improve the model by understanding better the trends and seasonality of each zip code. Therefore, a better understanding of the differencing levels for our model  
− I would explore other time series models such as Facebook Prophet, or Vector Autoregression Moving-Average with Exogenous Regressors model