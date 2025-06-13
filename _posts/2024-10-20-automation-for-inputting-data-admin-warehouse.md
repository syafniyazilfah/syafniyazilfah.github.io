---
title: Automation for Helping Admin Warehouse from Inputting Shipment Receipts Manual
tags: [Data, Python]
style: 
color: 
description: In a company where data collection is still manual and the process of automation is underway, there are numerous data-related issues that require correction and thorough cleaning.
---

So, my workspace is actually in the server room (yes, I know — ideally, it shouldn’t be there, but I’m part of the IT division, which consists of just four people). Besides the IT team, there’s also the warehouse admin working nearby, since the server room is right next to the product storage area where items are prepared for shipment to customers. Since requests for data are still relatively minimal, I often find myself observing what others are working on — whether I’m about to learn something new or lend a hand, no one really knows yet.

</br> Eventually, I started feeling tired watching the warehouse admin download PDF files from the marketplace to get shipment receipts, then manually copy-pasting each receipt’s data—such as destination address, purchased products, names, and so on—into spreadsheets.

</br>I investigated their work process and ended up learning a Python library specifically for extracting data from PDFs into Excel. I then processed the data using Google Colab so they could easily upload and download files without needing to install any software.

## I’m grateful that my colleague, who works as a warehouse admin, can now use their time for more important tasks, which helps save them from frequently working overtime.