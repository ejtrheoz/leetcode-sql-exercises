```
with base as(select requester_id id from RequestAccepted
union all
select accepter_id id from RequestAccepted)

SELECT *
FROM base 
```