```
SELECT  t1.reports_to AS employee_id ,
        t2.name,
        COUNT(t1.reports_to) AS reports_count,
        ROUND(AVG(t1.age)) AS average_age 

FROM Employees t1
JOIN Employees t2
ON t1.reports_to = t2.employee_id 
WHERE t1.reports_to IS NOT NULL
GROUP BY t1.reports_to
ORDER BY employee_id
```