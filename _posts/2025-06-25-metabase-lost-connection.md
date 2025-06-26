---
title: Lost Connection to Metabase While Have Present Tomorrow
tags: [Data, Backup Plan, Looker Studio, Metabase]
style: fill
color: light
description: CRM Manager need to present tomorrow but the Metabase lost connection, D-2 Hours before working hours end.
---

![](https://ik.imagekit.io/syafniya/lost%20connection.png?updatedAt=1750911366738)

## Struggle

1. For the past 4 days, I had been processing around **600K rows of data** to be visualized in a dashboard using **Metabase**, in preparation for a presentation scheduled for **9 AM the next day**.
2. Just when I had **5 charts left to compile**, an issue occurred: **Metabase failed to display even a single row**, just **2 hours before the end of the workday**.
3. I reported the issue to the **CRM Manager**, who escalated it to the **IT team**. The IT team suggested it was due to a **row display limit**.
4. However, I couldn’t fully accept that explanation because:
   - Metabase does have a known display limit of 2000 rows, **but in this case, not even one row or column appeared**.
   - If it were purely a limit issue, I **wouldn’t have been able to build the dashboard at all from the start** — not just fail at the end.

## Solution

1. With limited time and a presentation deadline looming, I shifted to an alternative approach:
   - I **processed and summarized the data using Python**.
   - Then I **exported the output to a spreadsheet**, which I connected to **Looker Studio** to build the dashboard.
2. Within **under 2 hours**, I managed to rebuild **90% of the dashboard**.
3. The remaining **10% was finalized the next morning**, roughly **40 minutes before working hours began**.
4. In the end, the dashboard was ready, and the **presentation went smoothly**.

## Final Result

- The dashboard was **delivered on time** and presented successfully.
- I was able to **solve the problem under pressure**.
- This situation demonstrated strong **adaptability**, **problem-solving**, and **time management** skills.
