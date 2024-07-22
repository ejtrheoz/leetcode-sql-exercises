```
SELECT class
FROM Courses
GROUP BY class
WHERE COUNT(student) >= 5;
```