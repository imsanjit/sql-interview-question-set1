# SQL Interview Question Set-1
### Data Set
Data Science Job Salaries

[Download data set here](https://www.kaggle.com/datasets/ruchi798/data-science-job-salaries)

---

1. You're a Compensation analyst employed by a multinational corporation. Your Assignment is to Pinpoint Countries who give work fully remotely, for the title 'managers’ Paying salaries Exceeding $90,000 USD
   ```
   SELECT DISTINCT(company_location)
          FROM
            salaries
          WHERE
            job_title LIKE '%manager%'
            AND remote_ratio = 100
            AND salary_in_usd > 90000;
   ```

    ![image](https://github.com/imsanjit/sql-interview-question-set1/assets/40655088/a40f2949-e60a-40cf-a054-1f3843955c74)


3. AS a remote work advocate Working for a progressive HR tech startup who place their freshers’ clients IN large tech firms. you're tasked WITH Identifying top 5 Country Having greatest count of large (company size) number of companies.
4. Picture yourself AS a data scientist Working for a workforce management platform. Your objective is to calculate the percentage of employees. Who enjoy fully remote roles WITH salaries Exceeding $100,000 USD, Shedding light ON the attractiveness of high-paying remote positions IN today's job market.
5. Imagine you're a data analyst Working for a global recruitment agency. Your Task is to identify the Locations where entry-level average salaries exceed the average salary for that job title IN market for entry level, helping your agency guide candidates towards lucrative opportunities.
6. You've been hired by a big HR Consultancy to look at how much people get paid IN different Countries. Your job is to Find out for each job title which. Country pays the maximum average salary. This helps you to place your candidates IN those countries.
7. AS a data-driven Business consultant, you've been hired by a multinational corporation to analyze salary trends across different company Locations. Your goal is to Pinpoint Locations WHERE the average salary Has consistently Increased over the Past few years (Countries WHERE data is available for 3 years Only(present year and past two years) providing Insights into Locations experiencing Sustained salary growth.
8.  Picture yourself AS a workforce strategist employed by a global HR tech startup. Your Mission is to Determine the percentage of fully remote work for each experience level IN 2021 and compare it WITH the corresponding figures for 2024, Highlighting any significant Increases or decreases IN remote work Adoption over the years.
9.  AS a Compensation specialist at a Fortune 500 company, you're tasked WITH analyzing salary trends over time. Your objective is to calculate the average salary increase percentage for each experience level and job title between the years 2023 and 2024, helping the company stay competitive IN the talent market.
