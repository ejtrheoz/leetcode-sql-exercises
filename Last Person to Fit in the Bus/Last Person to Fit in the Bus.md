```
WITH sum_table AS(
    SELECT  turn,
        person_name,
        weight,
        SUM(weight) OVER(ORDER BY turn) AS tot_weight
    FROM Queue
ORDER BY turn)


SELECT  TOP 1 person_name
FROM sum_table
WHERE tot_weight <= 1000
```