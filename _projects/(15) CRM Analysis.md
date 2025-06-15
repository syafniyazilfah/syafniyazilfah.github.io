---
name: CRM Analysis
tools: [SQL, Power Bi]
image: https://ik.imagekit.io/syafniya/newplot%20(2).png?updatedAt=1749955981244
description: Analysis that i did in my company before but with generated data by python
---

CRM analysis is an analysis that begins by understanding the customer lifecycle. It starts with advertising, which generates leads—where leads are customers who initiate communication with customer service due to their interest in the ads.

In this dataset, whenever a customer clicks on an ad, they are counted as a lead because it directly leads to communication with customer service. These leads will then convert into purchasers if the transaction is successful.

Therefore, it's necessary to generate dummy data consisting of ads data, leads data, and purchase data to perform this analysis.

````import pandas as pd
import numpy as np

np.random.seed(42)

start_date = '2024-01-01'
end_date = '2024-12-31'
dates = pd.date_range(start=start_date, end=end_date)

sources = ['Google', 'TikTok', 'Facebook']
campaigns_per_source = 3
sku_list = [f'SKU{i:03d}' for i in range(1, 11)]

# Generate campaigns
campaigns = []
for source in sources:
    for i in range(1, campaigns_per_source + 1):
        campaigns.append((source, f'{source}_Camp{i}'))

# Generate customer_id
customer_counter = 1

ads_data = []
leads_records = []
purchase_records = []
transaction_id = 1

for date in dates:
    for source, campaign in campaigns:
        impressions = np.random.randint(1000, 10000)
        clicks = np.random.randint(50, max(51, impressions // 10))

        spend = round(np.random.uniform(100, 1000), 2)

        # Leads = clicks, for unique customer_id 
        customer_ids = [f'CUST{customer_counter + i:07d}' for i in range(clicks)]
        customer_counter += clicks

        for cust_id in customer_ids:
            sku_interest = np.random.choice(sku_list)
            leads_records.append([date, cust_id, sku_interest, campaign, source])

        # Conversion 64% from leads to purchase
        num_purchase = int(clicks * 0.64)
        if num_purchase > 0:
            purchase_customers = np.random.choice(customer_ids, size=num_purchase, replace=False)

            for cust_id in purchase_customers:
                num_transactions = np.random.choice([1, 2, 3], p=[0.4, 0.4, 0.2])
                last_purchase_date = date

                for n in range(num_transactions):
                    if n == 0:
                        purchase_date = date
                    else:
                        gap_days = np.random.randint(7, 60)
                        purchase_date = last_purchase_date + pd.Timedelta(days=gap_days)
                        if purchase_date > dates[-1]:
                            purchase_date = dates[-1]

                    num_sku_bought = np.random.choice([1, 2], p=[0.7, 0.3])
                    skus_bought = np.random.choice(sku_list, size=num_sku_bought, replace=False)

                    for sku in skus_bought:
                        price = round(np.random.uniform(50, 500), 2)
                        qty = np.random.choice([1, 2, 3], p=[0.8, 0.15, 0.05])
                        purchase_records.append([
                            f'TXN{transaction_id:07d}',
                            purchase_date,
                            cust_id,
                            sku,
                            price,
                            qty,\
                        ])

                    transaction_id += 1
                    last_purchase_date = purchase_date

        ads_data.append([
            campaign,
            source,
            date,
            impressions,
            clicks,
            spend,
            clicks,
            round(spend / clicks, 2) if clicks > 0 else 0,
            num_purchase
        ])

df_ads = pd.DataFrame(ads_data, columns=[
    'campaign_id', 'source', 'date', 'impressions', 'clicks', 'spend', 'leads', 'cpl', 'conversions'
])
df_leads = pd.DataFrame(leads_records, columns=[
    'lead_date', 'customer_id', 'sku_interest', 'campaign_id', 'source'
])
df_purchase = pd.DataFrame(purchase_records, columns=[
    'transaction_id', 'purchase_date', 'customer_id', 'sku', 'price', 'qty'
])


````


After generating the data, I need to calculate the total purchase amount per customer, label whether a transaction is a first purchase, identify retention by checking for repeat purchases, and also flag second purchases if they occur within 45 days of the first purchase.

````uniquetx = cek[['customer_id', 'purchase_date', 'transaction_id']].drop_duplicates().sort_values(['customer_id', 'purchase_date', 'transaction_id'])
uniquetx['purchase_order'] = uniquetx.groupby('customer_id').cumcount() + 1


# for labelling transaction as first_purchase or retention
uniquetx = uniquetx.sort_values('purchase_order', ascending=False)
uniquetx['first_purchase'] = np.where(uniquetx['purchase_order']==1, 'yes', '')
uniquetx['retention'] = np.where(uniquetx['purchase_order']>=2, 'yes', '')

# for labelling trnasaction of second purchase in range 45 days after first_purchase
uniquetx['gap_days_since_first'] = (
  uniquetx['purchase_date'] - uniquetx.groupby('customer_id')['purchase_date'].transform('min')
).dt.days

uniquetx['second_purchase'] = np.where(
  (uniquetx['gap_days_since_first'] <= 65) & (uniquetx['purchase_order'] == 2), 'yes', ''
)

````

and the result will be like this

| transaction_id | purchase_date | customer_id | total  | amount  | purchase_order | first_purchase | retention | gap_days_since_first | second_purchase |
|----------------|---------------|-------------|--------|---------|----------------|----------------|-----------|----------------------|-----------------|
| TXN0000001     | 2024-01-01    | CUST0000016 | 466.90 | 538.54  | 1              | yes            |           | 0                    |                 |
| TXN0001878     | 2024-01-01    | CUST0001746 | 98.37  | 98.37   | 1              | yes            |           | 0                    |                 |
| TXN0001880     | 2024-01-01    | CUST0001696 | 148.38 | 148.38  | 1              | yes            |           | 0                    |                 |
| TXN0001882     | 2024-01-01    | CUST0001671 | 418.27 | 866.80  | 1              | yes            |           | 0                    |                 |
| TXN0001884     | 2024-01-01    | CUST0001677 | 303.46 | 500.86  | 1              | yes            |           | 0                    |                 |
| ...            | ...           | ...         | ...    | ...     | ...            | ...            | ...       | ...                  | ...             |
| TXN1065894     | 2024-12-31    | CUST0927262 | 434.93 | 1634.36 | 2              |                | yes       | 21                   | yes             |
| TXN0871594     | 2024-12-31    | CUST0758628 | 330.17 | 330.17  | 3              |                | yes       | 85                   |                 |
| TXN0936038     | 2024-12-31    | CUST0814528 | 495.26 | 495.26  | 3              |                | yes       | 65                   |                 |
| TXN0871616     | 2024-12-31    | CUST0758551 | 337.68 | 337.68  | 3              |                | yes       | 85                   |                 |
| TXN1132881     | 2024-12-31    | CUST0985650 | 460.04 | 460.04  | 1              | yes            |           | 0                    |                 |


I also need tiering to complete the customer lifecycle analysis in CRM. I’ve designed the tiering segmentation based on customer purchase behavior in the last 6 months, with the following criteria:

Power User: Total purchases over 2000 and more than 6 transactions.
Tier 3: Total purchases over 1000 with 4 or more transactions.
Tier 2: Total purchases over 600 with 3 or more transactions.
Tier 1: At least 1 purchase in the last 6 months, but total purchases under 550 and fewer than 2 transactions.

This segmentation helps in identifying high-value customers for targeted marketing and retention strategies.


````cutoff_date = pd.to_datetime('2024-12-31') - pd.DateOffset(months=6)
recent_purchase = cek[cek['purchase_date'] >= cutoff_date]

customer_cltv = recent_purchase.groupby('customer_id').agg(
    total_amount=('total', 'sum'),
    freq=('transaction_id', 'nunique')
).reset_index()

def assign_tier(row):
    if row['total_amount'] > 2000 or row['freq'] > 6:
        return 'Power User'
    elif row['total_amount'] > 1000 or row['freq'] >= 4:
        return 'Tier 3'
    elif row['total_amount'] > 600 or row['freq'] >= 3:
        return 'Tier 2'
    else:
        return 'Tier 1'

customer_cltv['tier'] = customer_cltv.apply(assign_tier, axis=1)

customer_cltv =customer_cltv[['customer_id', 'tier']]
cek = pd.merge(cek, customer_cltv, on='customer_id', how='left')
cek['tier'] = cek['tier'].fillna('No Tier')

````

I applied fillna() to anticipate cases where customers don’t have any purchases within the last 6 months. This ensures that these customers are still included in the dataset with a default tier label (e.g., 'No Tier'), making it easier to differentiate active from inactive customers during analysis. The result will be like this.

| transaction_id | purchase_date | customer_id | total  | amount  | purchase_order | first_purchase | retention | gap_days_since_first | second_purchase | tier    |
|----------------|---------------|-------------|--------|---------|----------------|----------------|-----------|----------------------|-----------------|---------|
| TXN0000001     | 2024-01-01    | CUST0000016 | 466.90 | 538.54  | 1              | yes            |           | 0                    |                 | No Tier |
| TXN0001878     | 2024-01-01    | CUST0001746 | 98.37  | 98.37   | 1              | yes            |           | 0                    |                 | No Tier |
| TXN0001880     | 2024-01-01    | CUST0001696 | 148.38 | 148.38  | 1              | yes            |           | 0                    |                 | No Tier |
| TXN0001882     | 2024-01-01    | CUST0001671 | 418.27 | 866.80  | 1              | yes            |           | 0                    |                 | No Tier |
| TXN0001884     | 2024-01-01    | CUST0001677 | 303.46 | 500.86  | 1              | yes            |           | 0                    |                 | No Tier |
| ...            | ...           | ...         | ...    | ...     | ...            | ...            | ...       | ...                  | ...             | ...     |
| TXN1065894     | 2024-12-31    | CUST0927262 | 434.93 | 1634.36 | 2              |                | yes       | 21                   | yes             | Tier 2  |
| TXN0871594     | 2024-12-31    | CUST0758628 | 330.17 | 330.17  | 3              |                | yes       | 85                   |                 | Tier 3  |
| TXN0936038     | 2024-12-31    | CUST0814528 | 495.26 | 495.26  | 3              |                | yes       | 65                   |                 | Tier 2  |
| TXN0871616     | 2024-12-31    | CUST0758551 | 337.68 | 337.68  | 3              |                | yes       | 85                   |                 | Tier 3  |
| TXN1132881     | 2024-12-31    | CUST0985650 | 460.04 | 460.04  | 1              | yes            |           | 0                    |                 | Tier 1  |

But how do i know the conversion from ads to leads to purchase? I need to merge 2 tables (leads, and purchase, because for lifecycle only need 2 of these) and visualize it with funnel chart

````leads = df_leads.groupby('lead_date')['customer_id'].nunique().sum()
df_leads_total = pd.DataFrame({'desc': ['Leads'], 'unique_customers': [leads]})

first_purchase = cek[cek['first_purchase'] == 'yes']['customer_id'].nunique()
df_first_purchase = pd.DataFrame({'desc': ['First Purchase'], 'unique_customers': [first_purchase]})
second_purchase = cek[cek['second_purchase'] == 'yes']['customer_id'].nunique()
df_second_purchase = pd.DataFrame({'desc': ['Second Purchase'], 'unique_customers': [second_purchase]})

tiering = cek[cek['tier'] != 'No Tier'].groupby('tier')['customer_id'].nunique().reset_index()
tiering = tiering.rename(columns={'tier': 'desc', 'customer_id': 'unique_customers'})
lifecycle_total = pd.concat([df_leads_total, df_first_purchase, df_second_purchase, tiering])

mapping = {
    'Leads': 1,
    'First Purchase': 2,
    'Second Purchase': 3,
    'Tier 1': 4,
    'Tier 2': 5,
    'Tier 3': 6,
    'Power User': 7
}
lifecycle_total['sorted_by'] = lifecycle_total['desc'].map(mapping)
lifecycle_total = lifecycle_total.sort_values('sorted_by').reset_index(drop=True)

lifecycle_total

````

and the result must be like this

| desc            | unique_customers | sorted_by |
|-----------------|------------------|-----------|
| Leads           | 985,858          | 1         |
| First Purchase  | 629,389          | 2         |
| Second Purchase | 377,702          | 3         |
| Tier 1          | 206,636          | 4         |
| Tier 2          | 100,726          | 5         |
| Tier 3          | 49,896           | 6         |
| Power User      | 1,839            | 7         |



and now funnel left

````import plotly.express as px

lifecycle_total = lifecycle_total.sort_values('sorted_by').reset_index(drop=True)

conversion_rates = [100] 
for i in range(1, len(lifecycle_total)):
    rate = lifecycle_total.loc[i, 'unique_customers'] / lifecycle_total.loc[i-1, 'unique_customers'] * 100
    conversion_rates.append(rate)

lifecycle_total['conversion_rate_%'] = conversion_rates

fig = px.funnel(lifecycle_total, x='unique_customers', y='desc', title='Customer Lifecycle Funnel with Conversion Rates')

for i, row in lifecycle_total.iterrows():
    fig.add_annotation(
        x=row['unique_customers'] + 0.6, 
        y=row['desc'],
        text=f"{row['conversion_rate_%']:.1f}%",
        showarrow=False,
        font=dict(color="black", size=12)
    )

fig.show()


````

and i got this

![](https://ik.imagekit.io/syafniya/newplot%20(2).png?updatedAt=1749955981244)
