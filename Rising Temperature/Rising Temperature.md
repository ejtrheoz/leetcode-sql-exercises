```
SELECT t2.id AS Id
FROM Weather t1
JOIN Weather t2
ON DATEDIFF(t2.recordDate , t1.recordDate ) = 1
AND t2.temperature > t1.temperature
```