SELECT Signups.user_id,
       ROUND(IFNULL(SUM(CASE WHEN action='timeout' THEN action=0 ELSE action=1 END)/COUNT(CASE WHEN action='timeout' THEN action=0 ELSE action=1 END), 0), 2) AS confirmation_rate 
FROM Signups 
LEFT JOIN Confirmations
ON Signups.user_id = Confirmations.user_id
GROUP BY user_id 