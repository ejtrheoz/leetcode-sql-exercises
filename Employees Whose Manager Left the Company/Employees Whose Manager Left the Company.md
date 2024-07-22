```
SELECT employee_id
FROM Employees 
WHERE salary < 30000 
AND manager_id NOT IN employee_id
ORDER BY employee_id
```