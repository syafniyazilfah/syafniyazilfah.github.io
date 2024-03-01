---
name: Data Analyst
tools: [Python]
image: https://i.ibb.co/r5TtfpM/01.png
description: Data Analyst based Walmart Data
---

![](https://i.ibb.co/r5TtfpM/01.png)

This is Walmart data that I use to analyst for
From that data we know that data have 8 column, there are :
Store = about label number of Store
Date = weekly date
Weekly_Sales = Sales for the given store in that week
Holiday_Flag = If it is a holiday week
Temperature = Temperature on the day of the sale
Fuel_Price = Cost of the fuel in the region
CPI = Consumer Price Index
Unemployment = Unemployment rate


I'm curious about the influence of temperature on weekly sales, then I want to know what the affect of Temperature for Weekly_Sales.
So, I did regression linear analysis between Temperature and Weekly_Sales

![](https://i.ibb.co/9vtpzQ0/02.png)

The scatter plot shows the relationship between Temperature and Weekly_Sales.
The red line represents a linear regression model that attempts to estimate how Weekly_Sales will change with changes in Temperature

![](https://i.ibb.co/K7LyD68/03.png)

And there are the coeff regression and the intercept

![](https://i.ibb.co/N1ySd9N/04.png)

After I got the coeff and intercept, I try to get predict of regression linear of Temperature and Weekly_Sales when the Temperature is 45 and I got the Weekly_Sales is 1077547.148

While checking the data for temperatures between 44-46, the data for weekly sales doesn't show a clear pattern, such as a definite increase or decrease.

![](https://i.ibb.co/518qgDQ/05.png)

Then, I conducted an R-squared score test to assess how temperature affects weekly sales, and I obtained a score of 0.0041, which is very low. Therefore, the conclusion regarding the relationship between temperature and weekly sales is that it is extremely weak.