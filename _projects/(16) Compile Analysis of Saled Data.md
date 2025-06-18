---
name: Analysis of Sales Data
tools: [Python]
image: https://ik.imagekit.io/syafniya/job_ai%204.png?updatedAt=1749818543007
description: The data I used for this portfolio is from generated data using python
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
2. Cohort Analysis
3. RFM
4. ARIMA
5. Behaviour Funnel


### 1. Descriptive Analysis
