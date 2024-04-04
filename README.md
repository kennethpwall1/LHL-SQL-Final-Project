                   # Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
To take an existing data set and perform exploratory analysis in postgreSQL and pgAdmin to answer questions provided and provide insights regarding the ecommerce dataset.

## Process
### Step1 - Reviewing Data in .csv Format and Creating the Database
I initially scanned the column data to see the information and what data types were necessary to setup the tables in pgAdmin
Mentor had suggested to use the most general datatype (text or numeric) as we can always cast later on.

### Step2 - Cleaning Data
The steps outlined in the process can be found in **cleaning_data.md**.

### Step3 - Starting with Questions
5 questions were asked for this project, which are included with the answers and SQL queries in **starting_with_questions.md**. Please see the documentation for answers provided and any commentary noted.

### Step4 - Starting with Data
Given the knowledge of the existing data we were to pose 3-5 questions with SQL queries to answer those questions. See questions, answers and SQL queries in **starting_with_data.md**.

### Step5 - Quality Assurance
As we explored the data to answer the questions I identified what were the risk areas and I identified and described them and the SQL queries used in **QA.md**.

### Step6 - Generate Database ERD
In pgAdmin, I generated the ERD for the database. See **schema.png** for the ecommerce database ERD created for this project.

### Step7 - Present the Results
Using the readme as a guide with the results from the queries we were to give a 5 min presentation on the process in the project and the reesults. Presentation powerpoint not provided in repository as all details can be found on GitHub.

## Results
### Starting with questions - Question 1 - Which cities and countries have the highest level of transaction revenues 


|country|total_revenue|
|-------|--------------|
|United States|	13154.17|
|Israel|        602|
|Australia|	    358|
|Canada	 |       150.15|
|Switzerland	|    16.99|

### Starting with questions - Question 2 - What is the average number of products ordered from visitors in each city and country
City
|city|	                        avg_units_sold|
|----|----------------------------------------|            
|San Bruno	                     |52.66666667|
|not available in demo dataset	|26.89726563|
|Mountain View	                |16.16513761|
|San Jose	                    |8.565217391|
|Salem	                        |7.545454545|
|New York	                    |6.895348837|
|Chicago	                     |   6.194117647|

|country|	        avg_units_sold|
|-------|-------------------------|
|United States|	19.24492151|
|Czechia|       5.18181818|
|Mexico	|        1.833333333|
|Canada	|        1.593406593|


### Starting with questions - Question 3 - s there any pattern in the types (product categories) of products ordered from visitors in each city and country?

|country|	    city|	                2productcategory|	                category_count|
|-------|-----------|-----------------------------------|---------------------------------|
|(not set)|	(not set)|	            Home/Apparel/Men's/	  |              1|
|(not set)|	(not set)|	            Home/Apparel/Men's/Men's-Outerwear/|	22|
|(not set)|	(not set)|	             Home/Bags/	|                        12|
|(not set)|	(not set)|	            Home/Shop by Brand/YouTube/	|        12|
|Albania|	    not available in demo dataset|	Home/Apparel/Men's/	|        23|
|Argentina|	Buenos Aires|	            Home/Bags/Backpacks/	    |    96|

Further exploration noted that almost all transactions were purchased by the USA and most products were either apparel or youtube related.

### Starting with questions - Question 4 - What is the top-selling product from each city/country? 
|country|	        city|	                        sku|	            top_selling|
|-------|---------------|------------------------------|---------------------------|
|United States|	not available in demo dataset|	GGOEAHPJ074410|	188|
|United States|	Charlotte	                  |  GGOEGBCR024399|	167|
|United States|	not available in demo dataset|	GGOEAHPA004110|	156|
|United States|	not available in demo dataset|	GGOEGAAX0231|	143|
|United States|	not available in demo dataset|	GGOEGAAX0098|	143|
|United States|	not available in demo dataset|	GGOEGHPB071610|	96|

All of the top 10 selling products were to the USA.

### Starting with questions - Question 5 - Can we summarize the impact of revenue generated from each city/country

|country	|        city|	                        2productcategory|	    sku	           | avg_units_sold	|top_selling_product|	total_revenue|
|-----------|------------|------------------------------------------|----------------------|----------------|-------------------|-------------|
|United States|	Sunnyvale	    |                Housewares	  |          GGOEGCBQ016499|	2.306818182|	    88|	    384999.32|
|United States|	not available in demo dataset|	Home/Nest/Nest-USA/	|    GGOENEBQ079199|	1.410714286|	    56|	    63571|
|United States|	not available in demo dataset|	Home/Nest/Nest-USA/	 |   GOENEBQ084699|	1.967741935	   | 31|	    22572|
|United States|	not available in demo dataset|	Home/Drinkware/	|GGOEYDHJ056099	      |  1.266666667|	    15|	    7228.61|
|United States|	Mountain View|	Waze	|                            GGOEWEBB082699	  |  1	        |    13|	    1149.44|
|United States|	New York|	Home/Apparel/Men's/Men's-Performance Wear/|	GGOEGAAX0591|	1	        |    12	|    6065.04|

### Starting with data - Question 1 - In the analytics table find the total number of unique visitors
|total_sessions	|unique_visistors|
|---------------|----------------|
|4301122	    |    120018|

Out of the tables 4.3M rows only 120k were unique visists

### Starting with data - Question 2 - What are the the total number of unique visitors by channel group

|channelgroup|	unique_visitors|
|------------|-----------------|
|Organic Search	|66333|
|Direct	        |21340|
|Referral	    |18382|
|Social	        |11023|
|Paid Search	|    3762|
|Affiliates	    |1469|
|Display	    |    844|
|(Other)	    |    2|

### Starting with data - Question 3 - What was the average time users spent on the site that have purchased a product
|fullvisitorid	|        avg_time_on_site|
|--------------|------------------------|
|8826538902252293768|	    8901.756972|
|7358671888562848931| 	8369|
|9919195169254003311|	    8230|
|3580472110818897042|	    7213|
|1864623622209203335|	    6909|


## Challenges 
1.) Direction in the project - not too sure what is expected in the project and what data should be used and if it is appropriate or relevant.
2.) Dataset - Most columns had empty/null values making it hard to know what solve for.
3.) Dataset - Need further information on the purpose of each column in each table and if they are even important.


## Future Goals
1.) I would explore more relationships between tables.
2.) Learn more about the Null values in each column and how we can potentially clean the data for these values before analysis.
3.) Spend more time solidifying the data types for each column, ie. being more specific.
4.) Practice SQL queries so cleaning and exploration are quicker.
5.) Ask more starting with data questions

