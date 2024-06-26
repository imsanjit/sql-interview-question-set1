# SQL Interview Question Set-1

### Data Set
Data Science Job Salaries

[Data set](https://www.kaggle.com/datasets/ruchi798/data-science-job-salaries)

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


2. AS a remote work advocate Working for a progressive HR tech startup who place their freshers’ clients in large tech firms. you're tasked WITH Identifying top 5 Country Having greatest count of large (company size) number of companies.
   ```
         SELECT 
             company_locatiON, COUNT(company_size) AS 'cnt'
         FROM
             (SELECT 
                 *
             FROM
                 salaries
             WHERE
                 experience_level = 'EN'
                     AND company_size = 'L') AS t
         GROUP BY company_locatiON
         ORDER BY cnt DESC
         LIMIT 5;
   ```

   ![image](https://github.com/imsanjit/sql-interview-question-set1/assets/40655088/988e68ca-3c19-421a-9ff2-643c4ae6b053)

3. Picture yourself AS a data scientist Working for a workforce management platform. Your objective is to calculate the percentage of employees. Who enjoy fully remote roles WITH salaries Exceeding $100,000 USD, Shedding light ON the attractiveness of high-paying remote positions in today's job market.

   ```
      SET @total = (SELECT COUNT(*) FROM salaries WHERE salary_in_usd>100000);
      SET @COUNT= (SELECT COUNT(*) FROM salaries  WHERE salary_in_usd >100000 AND remote_ratio=100);
      SET @percentage= round((((SELECT @COUNT)/(SELECT @total))*100),2);

      SELECT @percentage AS '%  of people working remotly and having salary >100,000 USD';
   ```
   ![image](https://github.com/imsanjit/sql-interview-question-set1/assets/40655088/9adb0366-f27c-41d8-a9f3-27c730c3e727)


   
4. Imagine you're a data analyst Working for a global recruitment agency. Your Task is to identify the Locations where average salaries exceed the average salary for that job title IN market for entry level, helping your agency guide candidates towards lucrative opportunities.
   
   ```
      SELECT 
          l.job_title,
          r.company_location,
          avg_salary,
          avg_per_contry_salary
      FROM
          (SELECT 
              job_title, AVG(salary) AS 'avg_salary'
          FROM
              salaries
          GROUP BY job_title) l
              INNER JOIN
          (SELECT 
              company_location,
                  job_title,
                  AVG(salary) AS 'avg_per_contry_salary'
          FROM
              salaries
          GROUP BY job_title , company_location) r ON l.job_title = r.job_title
      WHERE
          avg_per_contry_salary > avg_salary;
   
   ```
      ![image](https://github.com/imsanjit/sql-interview-question-set1/assets/40655088/0814983d-fa49-4ced-bb7f-bcffa789b018)


5. You've been hired by a big HR Consultancy to look at how much people get paid in different Countries. Your job is to Find out for each job title which. Country pays the maximum average salary. This helps you to place your candidates IN those countries.

   ```
      select *, dense_rank() over (partition by job_title order by avg_country_salary desc) as 'rank_num' 
         from 
         (
         select company_location, job_title, avg(salary) as 'avg_country_salary' 
         from 
         salaries 
         group by company_location, job_title
         )t 
         where rank_num = 1;

   ```
      ![image](https://github.com/imsanjit/sql-interview-question-set1/assets/40655088/6a75dd0c-1248-4eef-b164-4b17dabac1d3)

   
6. AS a data-driven Business consultant, you've been hired by a multinational corporation to analyze salary trends across different company Locations. Your goal is to Pinpoint Locations WHERE the average salary Has consistently Increased over the Past few years (Countries WHERE data is available for 3 years Only(present year and past two years) providing Insights into Locations experiencing Sustained salary growth.

   ```
      with cta_data as (
      	select * from salaries where company_location in
      	(select company_location from (
      	select company_location,  avg(salary) as 'avg_salary', count( distinct(work_year)) as 'cnt'
      	from salaries 
      	where work_year >= (year(current_date() )-2 ) 
      	group by company_location
      	having cnt = 3) t
      	)
          )
      select company_location, 
      max(case when work_year = 2022 then avg_salary end) avg_salary_2022,
      max(case when work_year = 2023 then avg_salary end) avg_salary_2023,
      max(case when work_year = 2024 then avg_salary end) avg_salary_2024
      from
      (
      select company_location, work_year, avg(salary) as 'avg_salary' from cta_data group by company_location, work_year
      )q group by company_location
      having avg_salary_2024 > avg_salary_2023 and avg_salary_2023 > avg_salary_2022
   ```
      ![image](https://github.com/imsanjit/sql-interview-question-set1/assets/40655088/b90cd4bc-f01a-44ab-8aa2-ec9ad1fecd64)

  
