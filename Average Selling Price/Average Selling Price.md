```
SELECT Prices.product_id,
       IFNULL(ROUND(SUM(price*units)/SUM(units), 2), 0) AS average_price
FROM Prices
LEFT JOIN UnitsSold
ON Prices.product_id = UnitsSold.product_id
AND DATEDIFF(Prices.start_date, UnitsSold.purchase_date ) <= 0
AND DATEDIFF(Prices.end_date, UnitsSold.purchase_date ) >= 0
GROUP BY Prices.product_id
```