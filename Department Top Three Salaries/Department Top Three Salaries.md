```
WITH sorted_table AS 
(SELECT  Department.name AS Department ,
        Employee.name AS Employee ,
        Employee.salary AS Salary ,
        DENSE_RANK() OVER(PARTITION BY Department.name ORDER BY Employee.salary DESC) AS rn
FROM Employee 
JOIN Department 
ON Employee.departmentId = Department.id)

SELECT  Department,
        Employee,
        Salary 
FROM sorted_table
WHERE rn <= 3
```