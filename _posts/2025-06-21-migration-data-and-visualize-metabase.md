---
title: New Era of Reading Data with Visualization in small business
tags: [Cleaning Data, Migration Data, Metabase]
style: info
color: 
description: Prepared data from raw data to visualization by doing cleaning and migration data.
---

At my company, we already had a database server where the warehouse team inputs sales data through a web system. But as I started preparing to build dashboards with Metabase, I realized that the database wasn’t ready for analysis.
1. The data was messy and unstructured.
2. There were testing records mixed with real data.
3. SKUs were inconsistent—different formats, typos, mixed naming.
4. Most importantly: the product data was combined in a single column.

For example, one transaction was recorded as a single row, and the product column contained a mix like:
"SKU-A 2 SKU-B 1 SKU-C 5"

This structure made it impossible to analyze product-level sales properly.

Meanwhile, the warehouse team was also maintaining manual spreadsheets for their daily operations. I decided to use those spreadsheets as my starting point, clean the data, and migrate it properly to a structured database.

**The Challenges**
1. Product columns contained combined SKUs and quantities → I needed to split them into separate rows.
2. SKU inconsistencies → typos, inconsistent naming.
3. Missing Customer IDs → no unique identifier to track customer behavior.
4. Most importantly: the product data was combined in a single column.
5. Existing database polluted with testing data → not usable for direct visualization.

**What I Did**
1. Collected the manual spreadsheet data from the warehouse team.
2. Processed it using Python:
3. Split product columns → one row for each product with its corresponding quantity.
4. Cleaned and standardized SKU names.
5. Generated unique customer IDs using a fallback logic:
    If phone number exists → use phone number.
    If phone is empty → use recipient’s name → or user’s name → or as a last fallback, use shipping address.
6. Migrated the cleaned data to a new MySQL database:
    Transactions Table → contains transaction info (date, channel, total amount, customer ID).
    Product Sales Table → one product per row, linked via transaction_id.
    After restructuring the data → connected it to Metabase for visualization.

**The Result**
1. Structured and cleaner database → no more errors in Metabase.
2. Built transaction and product-level dashboards for tracking marketplace and CS sales.
3. Provided a better foundation for further analytics and reporting in the company.
4. Successfully transformed unusable data into a reliable source for insights.

**What I Learned**
1. This project taught me that data visualization is only as good as the data underneath. Tools like Metabase are powerful, but they require clean, well-structured data to work properly.
2. It was also my first time combining roles of data cleaning, lightweight data engineering, and visualization in a single project.
