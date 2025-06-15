---
name: Analysis Job AI Dataset in Job Vacancy
tools: [SQL, Power Bi]
image: https://ik.imagekit.io/syafniya/job_ai%204.png?updatedAt=1749818543007
description: The data I used for this portfolio is data from Kaggle.
---

**Source Data:** [Global AI Job Market and Salary Trends 2025 - Kaggle](https://www.kaggle.com/datasets/bismasajjad/global-ai-job-market-and-salary-trends-2025)


### Cleaning data from raw data with query using MYSQL Workbench
<br />
After obtaining the data from Kaggle, since it was in CSV format, I needed to import it into MySQL Workbench. Once imported, I could see the columns in the table, which were as follows:
![](https://ik.imagekit.io/syafniya/job_ai%201.png?updatedAt=1749818542782)
<br /><br />
I noticed an interesting part of the data, which was the skills column. This column lists the skills required for each job position.
![](https://ik.imagekit.io/syafniya/job_ai%202.png?updatedAt=1749818542971)
<br /><br />

I wanted to clearly see how many AI-related job vacancies required each individual skill. However, since the data was still grouped together, it needed to be separated using the following query:
![](https://ik.imagekit.io/syafniya/job_ai%203.png?updatedAt=1749818542717)
<br /><br />

### Visualization data using Power Bi
<br />
After getting the separated data, I continued with the visualization using Power BI, connected to my local server (since I stored the data locally). In Power BI, I used DAX to add several additional columns to make the visuals easier to read — for example, grouping the year_experience column (which was originally just numbers), calculating the difference between the job opening and closing dates, and so on. Finally, I got the visualization result as shown below:
<br />
![](https://ik.imagekit.io/syafniya/job_ai%204.png?updatedAt=1749818543007)

<br />
<br />

From the data visualization, I was able to gather several insights, including:
1. Top Required Skills for AI Jobs:
<br />Python is by far the most in-demand skill (4,450 job postings), followed by SQL (3,407) and TensorFlow (3,022).
<br />Skills related to machine learning frameworks (PyTorch, TensorFlow, Kubernetes) and cloud platforms (GCP, AWS, Azure) are consistently required.

2. Job Vacancy Closing Time:
<br />70.94% of AI-related job vacancies are filled within more than 1 month, showing a high demand for talent and serious recruitment cycles.
<br />Only 1.57% take less than 2 weeks to close.

3. Salary by Employment Level:
<br /> EX positions have significantly higher average salaries, reaching around $200K.
<br /> Entry-level (EN) roles have the lowest average salaries.
<br /> As many people might expect, this can serve as a benchmark for salary expectations among job seekers.


5. Employee Citizenship:
<br />Around 28.37% of employees working in AI roles are foreigners, suggesting that companies are open to hiring international talent.
<br />71.63% of roles are filled by employees with citizenship in the company's country.

6. Years of Experience Required:
<br />0–4 years of experience is the most common requirement (~7.5K job postings).
<br />15–20 years of experience make up a smaller share (~1.8K postings).

7. Education Requirements:
<br />Education levels required are fairly evenly distributed between Bachelor’s, Master’s, and PhD across experience levels.
<br />EX roles slightly lean toward requiring a Master’s degree.

8. Company Size and Working Type:
<br />Regardless of company size (small, medium, or large), Hybrid working arrangements are the most common, slightly above 33% for each. 
<br />WFH (Work from Home) and WFO (Work from Office) share the remainder almost equally.
<br />That means even though the difference between WFH, WFO, and Hybrid is quite small, it’s clear here that Hybrid has the lowest proportion among the three. This suggests that most companies tend to prefer either fully WFH or fully WFO, rather than a mix of both.
