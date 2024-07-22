```
WITH managers AS (
     SELECT managerId,
       COUNT(managerId) AS managerCount
    FROM Employee
    WHERE managerId IS NOT NULL
    GROUP BY managerId
)

SELECT name
FROM Employee 
JOIN managers
ON managers.managerId = Employee.id
AND managerCount >= 5
```
