# Answer the following questions and provide the SQL queries used to find the answer.
  
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

SQL Queries:
```sql
SELECT
	country, 
	SUM(totaltransactionrevenue) AS total_revenue
FROM
	all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY country
ORDER BY total_revenue DESC
```
```sql
SELECT
	city, 
	SUM(totaltransactionrevenue) AS total_revenue
FROM
	all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY city
ORDER BY total_revenue DESC
```

Answer:
Country: USA $13,154.17. See readme file for details
City: Unknown $6,092.56. See readme file for details



**Question 2: What is the average number of products ordered from visitors in each city and country?**

SQL Queries:
```sql
SELECT
	country,
	AVG(unitssold) AS avg_units_sold
FROM
	all_sessions AS ses
JOIN
	analytics AS a on ses.fullvisitorid = a.fullvisitorid
WHERE unitssold is not null
GROUP BY country
ORDER BY avg_units_sold DESC
```
```sql
SELECT
	city,
	AVG(unitssold) AS avg_units_sold
FROM
	all_sessions AS ses
JOIN
	analytics AS a on ses.fullvisitorid = a.fullvisitorid
WHERE unitssold is not null
GROUP BY city
ORDER BY avg_units_sold DESC
```

Answer:
Country: USA - 19.24
City: San Bruno - 52.7


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```sql
SELECT
	country,
	city,
	v2productcategory,
	COUNT(v2productcategory) AS category_count
FROM
	all_sessions AS ses
JOIN
	analytics AS a on ses.fullvisitorid = a.fullvisitorid
GROUP BY country, city, v2productcategory
ORDER BY country
```
```sql
SELECT
	country,
	COUNT(
	CASE
		WHEN v2productcategory LIKE '%Apparel%' THEN 1
		ELSE 0
	END) AS apparel
FROM
	all_sessions AS ses
JOIN
	analytics AS a on ses.fullvisitorid = a.fullvisitorid
GROUP BY country
ORDER BY country
```

Answer:
I first counted the number of product category descriptions by country and city. Apparel and purchases to Youtube are the highest counts. As well as the USA buys a lot of random stuff as well that other countries do not buy, like pet, stickers, accessories.


## Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```sql
SELECT
	country,
	city,
	ses.productsku AS sku,
	COUNT(unitssold) AS top_selling
FROM
	all_sessions AS ses
JOIN
	analytics AS a on ses.fullvisitorid = a.fullvisitorid
JOIN
	sales_report AS sr on ses.productsku = sr.productsku
GROUP BY country, city, sku
ORDER BY top_selling DESC
```

Answer:
Country: USA - GGOEAHPJ074410 188 units
City: Charlotte USA GGOEGBCR024399 167 Units


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
```sql
SELECT
	country,
	city,
	ses.productsku AS sku,
	AVG(unitssold) AS avg_units_sold,
	count(unitssold) AS top_selling_product,
	SUM(totaltransactionrevenue) AS total_revenue
FROM
	all_sessions AS ses
JOIN
	analytics AS a on ses.fullvisitorid = a.fullvisitorid
GROUP BY country, city, totaltransactionrevenue, sku
ORDER BY top_selling_product DESC
```

Answer:
Top 10 selling products are all from the US the top selling products are in the US. See summary in readme file






