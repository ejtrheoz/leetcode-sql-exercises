```
WITH Low_Salary AS(
    SELECT  'Low Salary' AS category
),
Average_Salary AS(
    SELECT  'Average Salary' AS category
),
High_Salary AS(
    SELECT  'High Salary' AS category
),
table_1 AS (
    SELECT category
    FROM Low_Salary
    UNION
    SELECT category
    FROM Average_Salary
    UNION
    SELECT category
    FROM High_Salary
),
table_2 AS (
SELECT  category,
        COUNT(category) AS accounts_count 
FROM(
SELECT  CASE 
        WHEN income < 20000 THEN "Low Salary"
        WHEN (income >= 20000 AND income <= 50000) THEN "Average Salary"
        ELSE "High Salary" END AS category
FROM Accounts 
) AS Salary
GROUP BY category
)


SELECT  table_1.category,
        IFNULL(accounts_count, 0) AS accounts_count
FROM table_1
LEFT JOIN table_2
ON table_1.category = table_2.category



```