```
WITH potential_users AS
(
SELECT user_id
FROM
(SELECT  user_id,
        COUNT(user_id) AS cnt,
        RANK() OVER(ORDER BY COUNT(user_id) DESC) AS rn
FROM MovieRating
GROUP BY user_id) AS t1
WHERE rn = 1
),
first_answer AS (
    SELECT name
FROM Users
JOIN potential_users
ON potential_users.user_id = Users.user_id
ORDER BY name
LIMIT 1
),
second_answer AS(
SELECT title
FROM 
(SELECT  MovieRating.movie_id,
        AVG(rating) AS rating,
        title,
        RANK() OVER(ORDER BY AVG(rating) DESC) AS rn
FROM MovieRating
JOIN Movies 
ON MovieRating.movie_id = Movies.movie_id
WHERE EXTRACT(YEAR_MONTH FROM created_at) = 202002
GROUP BY movie_id 
) AS new_table
WHERE rn = 1
ORDER BY title
LIMIT 1
)

SELECT name AS results      
FROM first_answer
UNION ALL
SELECT title AS results
FROM second_answer


```