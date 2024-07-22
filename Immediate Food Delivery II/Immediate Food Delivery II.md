```
WITH ranked_table AS ( 
    SELECT customer_id,
       order_date,
       customer_pref_delivery_date,
       RANK() OVER(PARTITION BY customer_id ORDER BY order_date ) AS rn,
       CASE WHEN order_date = customer_pref_delivery_date THEN 1 ELSE 0 END AS immediate
    FROM Delivery
)

SELECT ROUND(SUM(immediate)/COUNT(*) * 100, 2) AS immediate_percentage 
FROM ranked_table
WHERE rn = 1
```