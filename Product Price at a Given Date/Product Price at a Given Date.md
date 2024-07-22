```
WITH part_table AS (SELECT  product_id,
        new_price AS price,
        change_date, 
        RANK() OVER(PARTITION BY product_id ORDER BY change_date DESC) AS rn
FROM Products
WHERE DATEDIFF(change_date, '2019-08-16') <= 0
),
filtrated_table AS(
    SELECT  product_id,
            price
    FROM part_table
    WHERE rn = 1
),
second_table AS (
    SELECT  product_id, 
            10 AS price
    FROM Products 
    WHERE product_id NOT IN (
        SELECT product_id
        FROM filtrated_table
    )
)

SELECT  product_id,
        price
FROM filtrated_table
UNION
SELECT  product_id,
        price
FROM second_table
```