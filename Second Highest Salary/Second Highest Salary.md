```
WITH temp AS(SELECT salary AS SecondHighestSalary 
FROM 
(SELECT  *,
        DENSE_RANK() OVER(ORDER BY salary DESC) AS rn
FROM Employee ) AS ranked
WHERE rn = 2)

SELECT IF(COUNT(*) = 0, NULL, SecondHighestSalary) AS SecondHighestSalary
FROM temp
```