```

SELECT  id,
        IFNULL(CASE WHEN id % 2 = 1 THEN for_odd ELSE for_even END, student ) AS student 
FROM (
SELECT *,
        LEAD(student, 1) OVER() AS for_odd,
        LAG(student, 1) OVER() AS for_even
FROM Seat
) AS t1
```