The data for this exercise has been derived from the `Indeed Data Scientist/Analyst/Engineer` [dataset](https://www.kaggle.com/elroyggj/indeed-dataset-data-scientistanalystengineer) on kaggle.com  

#### Provide the SQL queries and answers for the following questions/tasks using the data_analyst_jobs table you have created in PostgreSQL:

1.	How many rows are in the data_analyst_jobs table?

2.	Write a query to look at just the first 10 rows. What company is associated with the job posting on the 10th row?

3.	How many postings are in Tennessee? How many are there in either Tennessee or Kentucky?

4.	How many postings in Tennessee have a star rating above 4?

5.	How many postings in the dataset have a review count between 500 and 1000?

6.	Show the average star rating for each state. The output should show the state as `state` and the average rating for the state as `avg_rating`. Which state shows the highest average rating?

7.	Select unique job titles from the data_analyst_jobs table. How many are there?

8.	How many unique job titles are there for California companies?

9.	Find the name of each company and its average star rating for all companies that have more than 5000 reviews across all locations. How many companies are there with more that 5000 reviews across all locations?

10.	Add the code to order the query in #9 from highest to lowest average star rating. Which company with more than 5000 reviews across all locations in the dataset has the highest star rating? What is that rating?

11.	Find all the job titles that contain the word ‘Analyst’. How many different job titles are there? 

12.	How many different job titles do not contain either the word ‘Analyst’ or the word ‘Analytics’? What word do these positions have in common?


1.	How many rows are in the data_analyst_jobs table? 1793

SELECT COUNT (*)
FROM data_analyst_jobs;

2.	Write a query to look at just the first 10 rows. What company is associated with the job posting on the 10th row? XTO Land Data Analyst

SELECT *
FROM data_analyst_jobs
LIMIT 10;

3.	How many postings are in Tennessee? How many are there in either Tennessee or Kentucky? TN - 21   TN/KY – 27

SELECT COUNT (*)
FROM data_analyst_jobs
WHERE location = 'TN'

SELECT COUNT (*)
FROM data_analyst_jobs
WHERE location = 'TN' OR location = 'KY';

4.	How many postings in Tennessee have a star rating above 4? 3

SELECT COUNT (*)
FROM data_analyst_jobs
WHERE location = 'TN' AND star_rating > 4;

5.	How many postings in the dataset have a review count between 500 and 1000? 151

SELECT COUNT (*)
FROM data_analyst_jobs
WHERE review_count BETWEEN 500 and 1000;

6.	Show the average star rating for each state. The output should show the state as `state` and the average rating for the state as `avg_rating`. Which state shows the highest average rating? NE

SELECT location AS state, AVG(star_rating) as avg_rating
FROM data_analyst_jobs
GROUP BY state
ORDER BY avg_rating DESC;

7.	Select unique job titles from the data_analyst_jobs table. How many are there? 881 

SELECT DISTINCT title
FROM data_analyst_jobs;

8.	How many unique job titles are there for California companies? 230

SELECT DISTINCT title
FROM data_analyst_jobs
WHERE location = 'CA';

9.	Find the name of each company and its average star rating for all companies that have more than 5000 reviews across all locations. How many companies are there with more that 5000 reviews across all locations? 40

SELECT company, SUM(review_count) as review_count
FROM data_analyst_jobs
WHERE review_count > 5000
GROUP BY company
ORDER BY review_count DESC;

10.	Add the code to order the query in #9 from highest to lowest average star rating. Which company with more than 5000 reviews across all locations in the dataset has the highest star rating? What is that rating? Google 4.3

SELECT company, SUM(review_count) as review_count, AVG (star_rating) as avg_star_rating
FROM data_analyst_jobs
WHERE review_count > 5000
GROUP BY company
ORDER BY avg_star_rating DESC;

11.	Find all the job titles that contain the word ‘Analyst’. How many different job titles are there?  774

SELECT DISTINCT title
FROM data_analyst_jobs
WHERE title LIKE '%analyst%' OR
title LIKE '%Analyst%' OR
title LIKE '%ANALYST%';

12.	How many different job titles do not contain either the word ‘Analyst’ or the word ‘Analytics’? What word do these positions have in common? 4, Tableau

SELECT DISTINCT title
FROM data_analyst_jobs
WHERE title NOT LIKE '%analy%' AND
title NOT LIKE '%Analy%' AND
title NOT LIKE '%ANALY%';
