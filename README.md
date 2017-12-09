# SQL Common Table Expressions
## SQL CTE and nested CTE
```sql

WITH ct1 AS (
  SELECT
    project_id,
  	minimal_amount,
  	SUM(amount) AS sum_amount,
  	COUNT(donation.id)
  FROM donation JOIN project
  ON donation.project_id = project.id
  GROUP BY
  	project_id,
  	minimal_amount
  HAVING
  	SUM(amount) >= minimal_amount
  	AND COUNT(donation.id) > 10
    )
SELECT
	AVG(sum_amount)
FROM ct1;

```
```sql

WITH table1 AS (
	SELECT
  	c.region AS region,
  	ds.day AS day,
  	SUM(ds.customers) AS total_customers
  FROM daily_sales ds JOIN salesman s
  ON ds.salesman_id = s.id JOIN city c
  ON s.city_id = c.id
  GROUP BY 
  	c.region,
  	ds.day
  ), 
table2 AS (
	SELECT
    day,
    AVG(total_customers) AS avg_customers
   FROM table1
   GROUP BY day
	 )
    
SELECT
	day,
  avg_customers AS avg_region_customers
FROM table2
WHERE avg_customers = (SELECT MIN(avg_customers) FROM table2);
