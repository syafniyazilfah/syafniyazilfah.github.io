---
title: Overcoming Data Infrastructure Challenges for CRM Division
tags: [Data, SQL]
style: border
color: light
description: Addressing data integration challenges in a new CRM division.
---

A few weeks after being transferred to the newly formed CRM division, which requires extra data processing, I faced significant challenges related to data integration within the company. The CRM team relies on data from various sources, including advertising data and sales data, but these datasets were not yet fully integrated.

Prior to implementing an internal database system, most sales data from 2024 onward were manually maintained by the warehouse admin in spreadsheets. The company plans to implement a proper database system for tracking sales and inventory starting at the end of 2024.

One major obstacle was the absence of an Entity Relationship Diagram (ERD) for the existing database. Since the database was provided by an external vendor, detailed documentation such as ERD was not available. Understanding these table relationships is crucial for accurate data analysis.

Ideally, the backend team would create the ERD. However, due to limited internal resources and priorities, I took the initiative to:

1. Coordinate directly with stakeholders to clarify data needs,
2. Collaborate with the DBA to start mapping out table relationships,
3. Migrate spreadsheet data into SQL for easier processing,
4. Utilize Metabase for data visualization and structuring table relationships for clarity.

Through these efforts, I ensured that the CRM data analysis could continue smoothly despite incomplete infrastructure.
