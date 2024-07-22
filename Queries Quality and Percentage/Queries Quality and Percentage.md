```
WITH poor_query_percentage AS(
    SELECT query_name,
           COUNT(rating) AS count_bad
    FROM Queries
    WHERE rating < 3
    GROUP BY query_name
)

SELECT Queries.query_name,
       ROUND(SUM(rating/position)/COUNT(*), 2) AS quality,
       IFNULL(ROUND(count_bad/COUNT(*)*100, 2), 0) AS poor_query_percentage
FROM Queries
LEFT JOIN poor_query_percentage
ON poor_query_percentage.query_name = Queries.query_name
WHERE Queries.query_name IS NOT NULL
GROUP BY query_name
```