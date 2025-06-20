---
name: Analysis of Sales Data
tools: [Python]
image: https://ik.imagekit.io/syafniya/churn.png?updatedAt=1750292163344
description: The data I used for this portfolio is from generated data using python with Churn. RFM, Behaviour Funnel, and ARIMA
---

I was generated data of Ads Data, Leads Data, and Sales Data as below

this is the Ads Data result of the generated

<small>

| campaign_id   | source   | date       | impressions | clicks | spend  | leads | cpl  | conversions |
|---------------|----------|------------|-------------|--------|--------|-------|------|-------------|
| Google_Camp1  | Google   | 2024-01-01 | 8270        | 485    | 955.64 | 485   | 1.97 | 310         |
| Google_Camp2  | Google   | 2024-01-01 | 6501        | 185    | 496.54 | 185   | 2.68 | 118         |
| Google_Camp3  | Google   | 2024-01-01 | 3902        | 301    | 272.83 | 301   | 0.91 | 192         |
| TikTok_Camp1  | TikTok   | 2024-01-01 | 3339        | 310    | 984.18 | 310   | 3.17 | 198         |
| TikTok_Camp2  | TikTok   | 2024-01-01 | 6729        | 265    | 507.96 | 265   | 1.92 | 169         |
| TikTok_Camp2  | TikTok   | 2024-12-31 | 2043        | 168    | 188.46 | 168   | 1.12 | 107         |
| TikTok_Camp3  | TikTok   | 2024-12-31 | 2821        | 63     | 364.66 | 63    | 5.79 | 40          |
| Facebook_Camp1| Facebook | 2024-12-31 | 1477        | 122    | 569.51 | 122   | 4.67 | 78          |
| Facebook_Camp2| Facebook | 2024-12-31 | 3198        | 200    | 248.76 | 200   | 1.24 | 128         |
| Facebook_Camp3| Facebook | 2024-12-31 | 5679        | 291    | 440.48 | 291   | 1.51 | 186         |

</small>


this is the Leads Data result of the generated

<small>

| lead_date   | customer_id  | sku_interest | campaign_id    | source   |
|-------------|--------------|--------------|----------------|----------|
| 2024-01-01  | CUST0000001  | SKU008       | Google_Camp1   | Google   |
| 2024-01-01  | CUST0000002  | SKU005       | Google_Camp1   | Google   |
| 2024-01-01  | CUST0000003  | SKU007       | Google_Camp1   | Google   |
| 2024-01-01  | CUST0000004  | SKU010       | Google_Camp1   | Google   |
| 2024-01-01  | CUST0000005  | SKU003       | Google_Camp1   | Google   |
| 2024-12-31  | CUST0985854  | SKU001       | Facebook_Camp3 | Facebook |
| 2024-12-31  | CUST0985855  | SKU010       | Facebook_Camp3 | Facebook |
| 2024-12-31  | CUST0985856  | SKU004       | Facebook_Camp3 | Facebook |
| 2024-12-31  | CUST0985857  | SKU005       | Facebook_Camp3 | Facebook |
| 2024-12-31  | CUST0985858  | SKU006       | Facebook_Camp3 | Facebook |

</small>


and this is the Sales Data

<small>

| transaction_id | purchase_date | customer_id  | sku    | price  | qty |
|----------------|---------------|--------------|--------|--------|-----|
| TXN0000001     | 2024-01-01    | CUST0000016  | SKU009 | 466.90 | 1   |
| TXN0000001     | 2024-01-01    | CUST0000016  | SKU006 | 71.64  | 1   |
| TXN0000002     | 2024-01-18    | CUST0000016  | SKU001 | 211.47 | 2   |
| TXN0000002     | 2024-01-18    | CUST0000016  | SKU007 | 226.60 | 2   |
| TXN0000003     | 2024-03-03    | CUST0000016  | SKU002 | 222.75 | 1   |
| TXN1132878     | 2024-12-31    | CUST0985722  | SKU005 | 244.67 | 1   |
| TXN1132879     | 2024-12-31    | CUST0985722  | SKU008 | 198.79 | 1   |
| TXN1132879     | 2024-12-31    | CUST0985722  | SKU010 | 312.23 | 1   |
| TXN1132880     | 2024-12-31    | CUST0985722  | SKU003 | 305.59 | 1   |
| TXN1132881     | 2024-12-31    | CUST0985650  | SKU003 | 460.04 | 1   |

</small>

From 3 tables generated, i want to make few analysis based on them, the analysis that i want to do are :
1. Descriptive Analysis
2. Churn Analysis
3. RFM
4. ARIMA
5. Behaviour Funnel


### **1. Descriptive Analysis**
````
Total Impressions: 18235179
Total Clicks: 985858
Total Spend: 1796318.45
Total Unique Leads: 985858
Total unique customers purchase: 629389
Total Unique Purchases (transactions): 1132881
Total Revenue: 506630165.74
Overall Conversion Rate (purchases/leads): 114.91%
Average CPL: 1.82
````

The descriptive analysis indicates the presence of repeat purchases. This is reflected in the overall conversion rate of 114.91%, meaning there are approximately 15% more transactions than leads. In other words, for every 100 leads acquired, there are an average of 115 transactions, suggesting that some leads made multiple purchases.

### **2. Churn Analysis**

To perform Churn Analysis, I need to set a benchmark to determine when a customer is considered churned. I decided to define churn as having a last purchase **more than 90 days ago**.

````
reference_date = df_purchase['purchase_date'].max()

last_purchase = df_purchase.groupby('customer_id')['purchase_date'].max().reset_index()

churn_threshold = reference_date - timedelta(days=90)
last_purchase['churn'] = last_purchase['purchase_date'] < churn_threshold
````

The result obtained from the code is attached below.
![](https://ik.imagekit.io/syafniya/churn.png?updatedAt=1750292163344)

Out of ````629,389 unique purchasing customers````, 63.4% have churned, which means the number of churned customers is approximately 2 times greater than active customers.

To prevent further churn, especially within the 90-day window, we recommend regular retention initiatives, such as special events during payday or exclusive promotions (e.g., Black Market sales) at least once a month to recapture their attention.

Before launching campaigns, conducting behavioral analysis or customer surveys on churned users is essential to better understand their preferences, ensuring that the campaign is relevant, personalized, and impactful.


### **3. RFM**

First of all, i need to make a measure of Recency, Frequency, and Monetary values of each customer. i choose maximum date of the data purchase became the comparation for the Recency value.


````
reference_date = df_purchase['purchase_date'].max()

rfm = df_purchase.groupby('customer_id').agg({
    'purchase_date': lambda x: (reference_date - x.max()).days,
    'transaction_id': 'nunique',
    'price': 'sum'
}).rename(columns={'purchase_date': 'Recency', 'transaction_id': 'Frequency', 'price': 'Monetary'})

````

After got the Recency, Frequency, and Monetary values. I divided the Recency, Frequency, and Monetary values into 4 categories.

````
rfm['R_score'] = pd.qcut(rfm['Recency'], 4, labels=[4,3,2,1]).astype(int)

try:
    rfm['F_score'] = pd.qcut(rfm['Frequency'].rank(method='dense'), 4, labels=[1,2,3,4]).astype(int)
except ValueError:
    rfm['F_score'] = pd.cut(rfm['Frequency'], bins=4, labels=[1,2,3,4]).astype(int)

try:
    rfm['M_score'] = pd.qcut(rfm['Monetary'].rank(method='dense'), 4, labels=[1,2,3,4]).astype(int)
except ValueError:
    rfm['M_score'] = pd.cut(rfm['Monetary'], bins=4, labels=[1,2,3,4]).astype(int)

rfm['RFM_Score'] = rfm['R_score'].astype(str) + rfm['F_score'].astype(str) + rfm['M_score'].astype(str)
````

The reason I applied ````pd.qcut```` directly on the Recency score is because Recency is a continuous variable with a wide range of values, making it suitable for quantile-based binning without additional processing.

On the other hand, Frequency and Monetary scores are discrete variables. Frequency often has a relatively small set of possible values, and Monetary values can be highly skewed and unevenly distributed.

Because of this, to effectively split Frequency and Monetary into 4 meaningful categories, I first applied ranking ````(rank())```` to transform their discrete or skewed distributions into a more continuous-like scale. Then, I applied ````pd.qcut```` on these ranked values to get balanced quartile bins.

Then i need to make segmentation based on Recency, Frequency, and Monetary scores.

````
def segment_rfm(row):
    if row['RFM_Score'] == '444':
        return 'Champions'
    elif row['R_score'] >= 3 and row['F_score'] >= 3:
        return 'Loyal Customers'
    elif row['R_score'] >= 3 and row['M_score'] >= 3:
        return 'Big Spenders'
    elif row['R_score'] == 4:
        return 'Recent Customers'
    elif row['F_score'] >= 3:
        return 'Frequent Buyers'
    else:
        return 'At Risk'

rfm['Segment'] = rfm.apply(segment_rfm, axis=1)

````

And the result of the segmentation attached below

![](https://ik.imagekit.io/syafniya/pie%20chart%20RFM.png?updatedAt=1750290813133)

54% of our customers fall into the At Risk segment, meaning more than half of our customer base is at risk of churning or has significantly reduced engagement. This is a critical warning sign that immediate retention efforts are necessary to prevent revenue loss.

Recommendations:

Personalized engagement: Reach out with surveys or request feedback to make these customers feel valued and heard.

Targeted promotions: Offer incentives like discounts, vouchers, or free products to encourage reactivation.

Loyalty programs: Develop reward systems or communities to strengthen customer attachment and long-term loyalty.

For customers outside the At Risk segment:

Upselling and cross-selling: Promote new products with attractive offers such as buy-one-get-one or free samples.

Regular communication: Send relevant and engaging content tailored to their profile to maintain ongoing interest.


### **4. ARIMA**

The first step before processing data using the ARIMA method is to check the ADF test statistic and its p-value.

This is important to determine whether the data is stationary or not. In my case, the data I am using consists of monthly clicks.

````
from statsmodels.tsa.arima.model import ARIMA
from statsmodels.tsa.stattools import adfuller

df_ads['lead_month'] = pd.to_datetime(df_ads['date']).dt.to_period('M')
monthly_leads = df_ads.groupby('lead_month')['clicks'].sum()

result = adfuller(monthly_leads)
print('ADF Statistic:', result[0])
print('p-value:', result[1])

````

The results of the ADF test statistic and p-value are as follows:

````
ADF Statistic: -3.383983092868024
p-value: 0.011517156979879782
````

Since the p-value is less than 0.05, we can conclude that the data is already stationary. Therefore, no data transformation or differencing is needed.

Next, because no differencing or transformation is performed, the next step is to analyze the ACF and PACF plots to determine the appropriate orders of the Moving Average (MA) and Auto-Regressive (AR) components.

````
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 2, figsize=(12, 5))

plot_acf(monthly_leads, ax=axes[0])
axes[0].set_title('ACF')

plot_pacf(monthly_leads, ax=axes[1])
axes[1].set_title('PACF')

plt.show()

````

The code produced the following ACF and PACF plots:

![](https://ik.imagekit.io/syafniya/ACF%20PACF.png?updatedAt=1750377911596)

From the plots, it can be seen that both the ACF and PACF show a sharp decline after lag 0. Therefore, the possible ARIMA models could be ARIMA(0,0,0), ARIMA(1,0,0), ARIMA(0,0,1), or ARIMA(1,0,1).

Since several ARIMA models have been tested, the next step is to perform ARIMA analysis to determine the most suitable model.

This involves evaluating the models based on statistical metrics such as AIC, BIC, and residual diagnostics, in order to select the model that best fits the data.

##### ARIMA(0,0,0) Model Summary

| **Metric**               | **Value**       |
|--------------------------|-----------------|
| **Dependent Variable**   | clicks          |
| **Number of Observations** | 12              |
| **Model**                | ARIMA(0,0,0)    |
| **Log Likelihood**       | -115.750        |
| **AIC**                  | 235.501         |
| **BIC**                  | 236.471         |
| **HQIC**                 | 235.142         |



###### Coefficients


| **Variable** | **Coef**  | **Std Err** | **z**    | **P>|z|** | **[0.025** | **0.975]**  |
|--------------|-----------|-------------|----------|---------|------------|------------|
| const        | 82,150    | 1360.369    | 60.392   | 0.000   | 79,500     | 84,800     |
| sigma²       | 14,220,000| 8,760,000   | 1.624    | 0.104   | -2,940,000 | 31,400,000 |



###### Residual Diagnostics


| **Test**                 | **Value** | **Prob.** |
|--------------------------|-----------|-----------|
| Ljung-Box (L1) (Q)       | 0.20      | 0.66      |
| Jarque-Bera (JB)         | 1.16      | 0.56      |
| Heteroskedasticity (H)   | 0.25      | 0.21      |
| Skewness                 | 0.70      | -         |
| Kurtosis                 | 2.39      | -         |


##### ARIMA(1,0,0) Model Summary

| **Metric**               | **Value**       |
|--------------------------|-----------------|
| **Dependent Variable**   | clicks          |
| **Number of Observations** | 12              |
| **Model**                | ARIMA(1,0,0)    |
| **Log Likelihood**       | -115.687        |
| **AIC**                  | 237.374         |
| **BIC**                  | 238.829         |
| **HQIC**                 | 236.835         |



###### Coefficients


| **Variable** | **Coef**  | **Std Err** | **z**     | **P>|z|** | **[0.025** | **0.975]**  |
|--------------|-----------|-------------|-----------|---------|------------|------------|
| const        | 82,150    | 1036.453    | 79.265    | 0.000   | 80,100     | 84,200     |
| ar.L1        | -0.1076   | 0.257       | -0.418    | 0.676   | -0.612     | 0.397      |
| sigma²       | 14,680,000| 77,000      | 1.91e+08  | 0.000   | 14,700,000 | 14,700,000 |




###### Residual Diagnostics


| **Test**                 | **Value** | **Prob.** |
|--------------------------|-----------|-----------|
| Ljung-Box (L1) (Q)       | 0.04      | 0.84      |
| Jarque-Bera (JB)         | 1.12      | 0.57      |
| Heteroskedasticity (H)   | 0.22      | 0.17      |
| Skewness                 | 0.65      | -         |
| Kurtosis                 | 2.26      | -         |



##### ARIMA(0,0,1) Model Summary


| **Metric**               | **Value**       |
|--------------------------|-----------------|
| **Dependent Variable**   | clicks          |
| **Number of Observations** | 12              |
| **Model**                | ARIMA(0,0,1)    |
| **Log Likelihood**       | -114.933        |
| **AIC**                  | 235.865         |
| **BIC**                  | 237.320         |
| **HQIC**                 | 235.327         |



###### Coefficients


| **Variable** | **Coef**  | **Std Err** | **z**     | **P>|z|** | **[0.025** | **0.975]**  |
|--------------|-----------|-------------|-----------|---------|------------|------------|
| const        | 82,400    | 281.658     | 292.560   | 0.000   | 81,800     | 83,000     |
| ma.L1        | -0.9976   | 0.509       | -1.960    | 0.050   | -1.995     | ≈0         |
| sigma²       | 9,616,000 | ≈0          | 7.31e+10  | 0.000   | 9,620,000  | 9,620,000  |



###### Residual Diagnostics


| **Test**                 | **Value** | **Prob.** |
|--------------------------|-----------|-----------|
| Ljung-Box (L1) (Q)       | 1.17      | 0.28      |
| Jarque-Bera (JB)         | 0.26      | 0.88      |
| Heteroskedasticity (H)   | 0.33      | 0.31      |
| Skewness                 | 0.01      | -         |
| Kurtosis                 | 2.28      | -         |



##### ARIMA(1,0,1) Model Summary

| **Metric**               | **Value**       |
|--------------------------|-----------------|
| **Dependent Variable**   | clicks          |
| **Number of Observations** | 12              |
| **Model**                | ARIMA(1,0,1)    |
| **Log Likelihood**       | -114.211        |
| **AIC**                  | 236.421         |
| **BIC**                  | 238.361         |
| **HQIC**                 | 235.703         |



###### Coefficients


| **Variable** | **Coef**  | **Std Err** | **z**     | **P>|z|** | **[0.025** | **0.975]**  |
|--------------|-----------|-------------|-----------|---------|------------|------------|
| const        | 82,340    | 405.650     | 202.994   | 0.000   | 81,500     | 83,100     |
| ar.L1        | 0.3605    | 0.298       | 1.209     | 0.227   | -0.224     | 0.945      |
| ma.L1        | -1.0000   | 0.656       | -1.524    | 0.128   | -2.286     | 0.286      |
| sigma²       | 9,245,000 | ≈0          | 1.3e+14   | 0.000   | 9,250,000  | 9,250,000  |



###### Residual Diagnostics


| **Test**                 | **Value** | **Prob.** |
|--------------------------|-----------|-----------|
| Ljung-Box (L1) (Q)       | 0.09      | 0.77      |
| Jarque-Bera (JB)         | 0.71      | 0.70      |
| Heteroskedasticity (H)   | 0.27      | 0.23      |
| Skewness                 | 0.14      | -         |
| Kurtosis                 | 1.84      | -         |


From the four models, the best model is ARIMA(0,0,0), as indicated by the lowest AIC value, the lowest BIC value, and the log likelihood value closest to zero compared to the other models.

However, the drawback of this model compared to others lies in its relatively large sigma² value. Since sigma² only affects the variability of the forecasted results, the weakness of ARIMA(0,0,0) is that its predictions tend to be less stable. Nevertheless, its advantages in terms of AIC, BIC, and Log Likelihood make ARIMA(0,0,0) superior to the other models.


### **5. Behaviour Funnel**

I have data for behaviour funnel, using impressions, clicks, leads, and transaction

````
Impressions: 18235179
Clicks: 985858 (CTR: 5.41%)
Leads: 985858 (Lead Conversion: 100.00%)
Purchases: 1132881 (Purchase Conversion: 114.91%)
````

and the funnel will show as this
![](https://ik.imagekit.io/syafniya/newplot.png?updatedAt=1750291325204)

The significant gap between impressions and clicks indicates an opportunity for improvement. To increase engagement, we should create more interactive ads that truly resonate with the audience—ads that reflect their interests and follow current trends.

For example, if our product targets Gen Z, the ad content must align with trends popular among this group. Additionally, fine-tuning ad settings such as age, gender, and other demographics will help us reach the right customers more effectively.

By tailoring both the creative content and the targeting settings, we can increase click-through rates and ultimately generate more leads.
