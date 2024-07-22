```
WITH 
first_login AS(
SELECT player_id,
       event_date,
       RANK() OVER(PARTITION BY player_id ORDER BY event_date) AS rn
FROM Activity
),
continuous_attending AS( 
SELECT DISTINCT t2.player_id,
       t2.event_date
FROM Activity t1
JOIN Activity t2
ON DATEDIFF(t1.event_date, t2.event_date) = 1
AND t1.player_id = t2.player_id 
ORDER BY t1.player_id
),
target_amount AS(
SELECT COUNT(*) AS target_amount
FROM first_login
JOIN continuous_attending
ON first_login.event_date =  continuous_attending.event_date
AND first_login.player_id = continuous_attending.player_id 
WHERE rn = 1
)


SELECT ROUND(target_amount/COUNT(DISTINCT player_id), 2) AS fraction 
FROM Activity, target_amount

```