# What are your risk areas? Identify and describe them.
1.) Ensuring data is complete (no blank or null values)
    This entire dataset was a risk area. Over half of the columns were incomplete or were filled with null values, which makes it difficult to determine if that was done on purpose or if data is actually missing. It makes it difficult to do data analysis when over half of the data is null values.
2.) Values should be unique.
    For all the product related tables a primary key was identified so all of the SKU data was unique within each table. However, there seems to be some redundancy across tables. the sales_by_sku and the sales_report tables both have total ordered. It is unclear if one is for one ordered by the company and one is order by the customer as some of the values are the same. Need to follow up.
3.) Consistent.
    Some of the actual transaction related columns I think should be initialized to zero even if there are no purchases as it makes no sense for a quantity to be null. See queries below
    Also, when reviewing the sentiment score, I noticed that some of the values are negative. We would just need to confirm that that is a possible value. If negatives aren't allowed we can write a case statement below

## QA Process:
Describe your QA process and include the SQL queries used to execute it.

### 1.) Determining the number of null values in a column
```sql
SELECT 
	COUNT(*)
FROM
	all_sessions
WHERE fullvisitorid is NULL
```

### Setting totaltransactionrevenue column null values to zero and divide by $1M
Transaction revenue should never be null. A zero value is used to replace all transactions that took place with no revenue transaction.
```sql
SELECT 
	CASE
		WHEN totaltransactionrevenue IS NULL THEN 0
		ELSE totaltransactionrevenue / 1000000
	END AS total_txn_revenue
FROM all_sessions
```

### Setting transactions column null values to zero
Transactions should never be null. A zero value is used to replace all transactions that took place with no transaction value.
```sql
SELECT 
	CASE
		WHEN transactions IS NULL THEN 0
		ELSE transactions
	END AS transactions
FROM all_sessions
```

### Setting timeonsite column null values to zero
Time on site should never be null. A zero value is used to replace all time on site that took place with no value.
```sql
SELECT 
	CASE
		WHEN timeonsite IS NULL THEN 0
		ELSE timeonsite
	END AS timeonsite
FROM all_sessions
```

### Setting productquantity column null values to zero
product quantity should never be null. A zero value is used to replace all quanity that took place with no value.
```sql
SELECT 
	CASE
		WHEN productquantity IS NULL THEN 0
		ELSE productquantity
	END AS productquantity
FROM all_sessions
```

## SALES REPORT TABLE
QA - negative sentiment score possible?
```sql
SELECT 
	CASE
		WHEN sentimentscore < 0 THEN 0
		ELSE sentimentscore
	END AS sentimentscore
FROM sales_report