---
name: Data Analysis of Sinergi Group
tools: [Python, PostgreSQL]
image: https://i.ibb.co.com/3dq0JYN/Screenshot-2024-11-05-132131.png
description: The data I used for this portfolio is dummy data.
---

### Forecastiong of the dataset B2B using ARIMA (python)

![](https://i.ibb.co.com/3dq0JYN/Screenshot-2024-11-05-132131.png)
<br />
The first step after cleaning the data is to check it by examining the p-value. As we can see, the p-value is lower than 0.05, which indicates that the data is stationary. Therefore, we can proceed to use the real data for forecasting.

<br />
Next, the Partial Autocorrelation Function (PACF) and Autocorrelation Function (ACF) are required to determine the ARIMA model.
<br />

![](https://i.ibb.co.com/V9HB9J2/acf.png)
![](https://i.ibb.co.com/zSDrzx4/pacf.png)
<br />
It is observed that the PACF begins to approach 0 after lag 2 and lag 3, and the same pattern is seen in the ACF. Therefore, the following ARIMA models are proposed: (2,0,2), (2,0,3), (3,0,2), and (3,0,3).

<br />
From these four models, the following errors were obtained:
<br />
![](https://i.ibb.co.com/9HR9f12/Screenshot-2024-11-05-132859.png)
<br />
From the three error calculations, it is evident that the ARIMA(3,0,3) model has the lowest error values for RMSE and MSE. Therefore, the model that will be used for forecasting sales revenue is ARIMA(3,0,3) to estimate the sales revenue for the next 30 days, utilizing data from the last 10 months.

### Trend Analysis of the dataset B2B

![](https://i.ibb.co.com/JBYYSWH/Screenshot-2024-11-05-131009.png)
<br />
To examine the presence of seasonality in the trend, the following plot was obtained:
<br />
![](https://i.ibb.co.com/GHPRsyH/newplot.png)
<br />
It can be seen that there is no seasonal trend in sales revenue, so a deeper analysis is needed to understand when trends rise and fall.

<br />
Upon examining the specific dates when these fluctuations occur, it turns out these dates do not align with any events. Therefore, it can be concluded that B2B purchases drive this trend, based on each agent’s cash flow. This conclusion stems from further data analysis showing that certain agents purchase more than four times in a single month, but then only once—or not at all—in the following months. Occasionally, there is a single, large purchase within a month.
<br />
To address this, the sales team could coordinate with the partnership team to negotiate and create promotions for B2B or agents by linking them to event dates, encouraging more consistent purchasing behavior.
