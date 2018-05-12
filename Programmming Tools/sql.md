# Basic Idea of SQL, Structure Query Language
## Basic Database Object: a table:
 |     |             | Table Name |   |     |         |  
 | --- | -------     |  ------- | --- | --- | ------- |  
 |     | colunm 1    | column 2 | ... |...  | column 3|
 |     | data 1-1    | data 2-1 |     |     | data 3-1 |
 |     | ...    | ... |     |     | ... |  
 |     | data 1-N    | data 2-N |     |     | data 3-N |
 

> All the data in the same column must match in terms of **data type**.  
>> Make SQL work fast.

## SELECT ... FROM ... :  Statement for reading data.
* SELECT: Allowed to read data and display.   
> Must common **STATEMENT** for database anaysis.  
> Rules:  
>* STATEMENT should be uppercase. Others are lowercase.  
>* SQL ignore white spaces, so it's same if you add blank line within.
>* Add " ; " in the end of statement.
```sql
 SELECT cloumn_name FROM table_name_; 
```
* Other STATEMENT: Create a new table / Remove a Table
```sql
CREATE / DROP
```

## ORDER BY: Query in Order
| | TWO TYPE |
---|---   
|ORDER BY| Increasing Order|  
ORDER BY ... DESC| Descending Order
EX: Take the  **5 Newest** data and it got higher total_amt_use in its day.
```sql
SELECT *
FROM orders
ORDER BY occurred_at DESC, total_amt_usd DESC
LIMIT 5;
```
EX: Take the  **10 OLDEST** data and it got smallest total_amt_use in its day.

```sql
SELECT *
FROM orders
ORDER BY occurred_at, total_amt_usd
LIMIT 10;
```
 ## Where: Allow you to Filter a Set of Result based on Specific Critia.
 EX: Select 5 data whose gloss_amt_usd > 1000 from the orders sheet 
 ```sql
SELECT *
FROM orders
WHERE gloss_amt_usd >= 1000
LIMIT 5;
```
 EX: Access data with non-numeric info.
 ```sql
SELECT name, website, primary_poc
FROM accounts
where name = 'Exxon Mobil';
```
### Logical Tool for non-numerical data
* LIKE
* IN
* NOT
* AND & BETWEEN
* OR  
EX: Access data whose name starts with 'C'
```sql
SELECT name
FROM accounts
WHERE name LIKE 'C%';
```
EX: Access data whose name not starts with 'C'
```sql
SELECT name
FROM accounts
WHERE name NOT LIKE 'C%'
```
EX: Name with 'one' 
```sql
SELECT name
FROM accounts
WHERE name LIKE '%one%';
```
EX: IN, Non-numerical list for search 
```sql
SELECT name, primary_poc, sales_rep_id
FROM accounts
WHERE name IN ('Walmart', 'Target', 'Nordstrom')
```
EX: AND: use two condition 
```sql
SELECT *
FROM accounts
WHERE name NOT LIKE 'C%' AND name NOT LIKE '%S'
ORDER BY name;
```
EX: Between: use for time period
```sql
SELECT *
FROM web_events
WHERE channel IN ('organic', 'adwords') AND occurred_at BETWEEN '2016-01-01' AND '2017-01-01'
ORDER BY occurred_at DESC;
```
EX: How to MIX AND, OR clearly.
```sql
SELECT *
FROM accounts
WHERE (name LIKE 'C%' OR name LIKE 'W%') 
           AND ((primary_poc LIKE '%ana%' OR primary_poc LIKE '%Ana%') 
           AND primary_poc NOT LIKE '%eana%');
```
## Derive : select several columns to form a new one.
EX: New Column for unit price.
```sql
SELECT 
	id, 
    account_id,
    standard_amt_usd / standard_qty AS unit_price
FROM orders
LIMIT 10;
```

## Recap

|**Statement**|	How to Use It|	Other Details|
| --- | --- | --- |
SELECT|	SELECT Col1, Col2, ...|Provide the columns you want
FROM	|FROM Table	|Provide the table where the columns exist
LIMIT	|LIMIT 10	|Limits based number of rows returned
ORDER BY|	ORDER BY Col	|Orders table based on the column. Used with DESC.
WHERE	|WHERE Col > 5	|A conditional statement to filter your results
LIKE	|WHERE Col LIKE '%me%	|Only pulls rows where column has 'me' within the text
IN	|WHERE Col IN ('Y', 'N')	|A filter for only rows with column of 'Y' or 'N'
NOT	|WHERE Col NOT IN ('Y', "N')	|NOT is frequently used with LIKE and IN
AND	|WHERE Col1 > 5 AND Col2 < 3	|Filter rows where two or more conditions must be true
OR	|WHERE Col1 > 5 OR Col2 < 3	|Filter rows where at least one condition must be true
BETWEEN	|WHERE Col BETWEEN 3 AND 5	|Often easier syntax than using an AND

* SQL is not case sensitive (it doesn't care if you write your statements as all uppercase or lowercase)
* The order of the key words does matter! 

### Source:
> Udacity - Data Analyst Nanodegree Program, Term 1 Material.