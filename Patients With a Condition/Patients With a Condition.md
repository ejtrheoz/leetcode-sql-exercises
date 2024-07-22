```
SELECT *
FROM Patients 
WHERE conditions LIKE '%DIAB1%'
AND conditions NOT LIKE '%SADIAB100%'
```