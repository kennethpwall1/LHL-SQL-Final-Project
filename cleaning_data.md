# What issues will you address by cleaning the data?
1.) I ensured accurate datatypes when creating the tables in pgAdmin. Text, numeric, dates, etc.
2.) Removed irrelevant observations:
    > Several columns in the all_sessions table and analytics tables only contained null values and were dropped. See queries below.
    > I was unable to determine a primary key in the all_sessions or analytics tables due to duplicate occurences for: fullvisitorid, date, visitid if different pages were viewed
3.) Address missing values:
    > Country or City columns with "(not set)" were either set to unkown or to the country name. See query below
    > Most of the database tables are missing or have null values so it is difficult to determine what should be included where a null value currently is. Some further null value initializing will be discussed in the QA.md document.
4.) Fixing Typos
    > productprice, productrevenue, totaltransactionrevenue should all be divided by 1M. See query below.

# Queries:
Below, provide the SQL queries you used to clean your data.

## Sessions Table

### Determining the number of null values in a column
```sql
SELECT 
	COUNT(*)
FROM
	all_sessions
WHERE fullvisitorid is NULL
```

### Setting and country and city column values using CASE statements
There are several rows that have data so I have decided to keep the records using the "unknown" text value in the cell value to identify

```sql
SELECT
	CASE
		WHEN
			country = '(not set)' THEN 'unknown'
		else
			country
	END as country
FROM all_sessions
```

```sql
SELECT
	CASE
		WHEN country = '(not set)' THEN 'unkown'
		WHEN city = '(not set)' THEN country
		WHEN city = 'not available in demo dataset' THEN country
		ELSE city
	END AS city
FROM all_sessions
```

### Productrefundamount column NULL values
This column has all null values and provides no value so it is to be dropped from the table.

```sql
ALTER TABLE all_sessions
DROP COLUMN IF EXISTS productrefundamount
```

### Dividing productprice column by 1M as instructed
```sql
SELECT 
	productprice / 1000000 AS productprice
FROM
	all_sessions
```

### Setting productrevenue column null values to zero and dividing values by 1M as instructed
product revenue should never be null. A zero value is used to replace all quanity that took place with no value.
```sql
SELECT 
	CASE
		WHEN productrevenue IS NULL THEN 0
		ELSE productrevenue / 1000000
	END AS productrevenue
FROM all_sessions
```

### itemquantity column NULL values
This column has all null values and provides no value so it is to be dropped from the table.

```sql
ALTER TABLE all_sessions
DROP COLUMN IF EXISTS itemquantity
```

### itemrevenue column NULL values
This column has all null values and provides no value so it is to be dropped from the table.

```sql
ALTER TABLE all_sessions
DROP COLUMN IF EXISTS itemquantity
```

### Setting transactionrevenue column null values to zero and divide by $1M
Transaction revenue should never be null. A zero value is used to replace all transactions that took place with no revenue transaction.
```sql
SELECT 
	CASE
		WHEN transactionrevenue IS NULL THEN 0
		ELSE transactionrevenue / 1000000
	END AS transactionrevenue
FROM all_sessions
```

### Setting the one pagetitle column value not set to the product category
```sql
SELECT 
	CASE
		WHEN pagetitle = '(not set)' THEN v2productcategory
		WHEN pagetitle IS NULL THEN v2productcategory
		ELSE pagetitle
	END pagetitle
FROM
	all_sessions
```

### searchkeyword column NULL values
This column has all null values and provides no value so it is to be dropped from the table.

```sql
ALTER TABLE all_sessions
DROP COLUMN IF EXISTS searchkeyword
```


## ANALYTICS TABLE
### userid column NULL values
This column has all null values and provides no value so it is to be dropped from the table.
```sql
ALTER TABLE analytics
DROP COLUMN IF EXISTS userid
```


