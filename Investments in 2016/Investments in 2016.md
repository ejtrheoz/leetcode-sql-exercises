```
WITH shared_tiv_ids AS (
    SELECT  DISTINCT t1.pid,
            t1.tiv_2016 
FROM Insurance t1
JOIN Insurance t2
ON t1.tiv_2015 = t2.tiv_2015
AND t1.pid != t2.pid),

forbidden_ids AS
(SELECT DISTINCT t1.pid
FROM Insurance t1
JOIN Insurance t2
ON t1.lat = t2.lat
AND t1.lon = t2.lon
AND t1.pid != t2.pid)

SELECT  ROUND(SUM(tiv_2016), 2) AS tiv_2016
FROM shared_tiv_ids
WHERE pid NOT IN (
    SELECT pid
    FROM forbidden_ids
)
```