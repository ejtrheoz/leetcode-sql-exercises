```
SELECT t1.machine_id,
       ROUND(SUM(t2.timestamp - t1.timestamp)/COUNT(t1.machine_id), 3) AS processing_time
FROM Activity t1
JOIN Activity t2
ON t1.process_id = t2.process_id 
AND t1.machine_id = t2.machine_id
AND t1.activity_type = "start"
AND t2.activity_type = "end"
GROUP BY t1.machine_id
```