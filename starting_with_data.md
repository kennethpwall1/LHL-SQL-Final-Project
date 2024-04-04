


## Question 1: In the analytics table find the total number of unique visitors

SQL Queries:
```sql
SELECT
	COUNT(*) AS total_sessions,
	COUNT( DISTINCT fullvisitorid) AS unique_visistors
FROM
	analytics
```
Answer: 
There were 4.3M rows in the table and out of them 120,018 represent unique visitor IDs


## Question 2: What are the the total number of unique visitors by channel group

SQL Queries:
```sql
SELECT
	channelgroup,
	COUNT( DISTINCT fullvisitorid) AS unique_visitors
FROM
	analytics
GROUP BY channelgroup
ORDER BY unique_visitors DESC
```

Answer:
Oraganic Search: 66,333
Direct: 21,340
Referral: 18,382


## Question 3: What was the average time users spent on the site that have purchased a product
SQL Queries:
```sql
SELECT 
	fullvisitorid,
	AVG(timeonsite) AS avg_time_on_site
FROM
	analytics
WHERE unitssold is not null
GROUP BY fullvisitorid
ORDER BY avg_time_on_site DESC
```
Answer:
Query above is the average time for each user, but the average time for all users who have purchased a product is 1220 milliseconds


