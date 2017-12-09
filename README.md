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
