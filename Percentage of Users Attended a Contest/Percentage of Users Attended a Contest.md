```
WITH total_users AS (
    SELECT COUNT(*) AS cnt
    FROM Users 
)

SELECT contest_id,
       ROUND(COUNT(user_id)/total_users.cnt *100, 2) as percentage
FROM Register, total_users
GROUP BY contest_id 
ORDER BY percentage DESC, contest_id ASC
```