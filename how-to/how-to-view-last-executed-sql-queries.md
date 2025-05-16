---
tags: sql, ssms
---

# How to view last executed queries in SSMS 2019

If you want to access the list of queries executed on a specific database (in this case, `proveDavide`), use this query.

```sql
SELECT 
    DB_NAME(CONVERT(INT, pa.value)) AS DatabaseName,
    st.text AS SQLText,
    qs.execution_count,
    qs.total_elapsed_time / qs.execution_count AS AvgElapsedTime,
    qs.creation_time,
    qs.last_execution_time
FROM 
    sys.dm_exec_query_stats AS qs
CROSS APPLY 
    sys.dm_exec_sql_text(qs.sql_handle) AS st
CROSS APPLY 
    sys.dm_exec_plan_attributes(qs.plan_handle) AS pa
WHERE 
    pa.attribute = 'dbid' 
    AND CONVERT(INT, pa.value) = DB_ID('proveDavide') 
ORDER BY 
    qs.last_execution_time DESC;

```

It returns the list of queries executed on the DB, as well as its duration.

But it does not resolve variables, and some queries appear like this:

```text
(@promoId nvarchar(4000),@customerId nvarchar(4000),@productEan nvarchar(4000),@status nvarchar(4000),@lastUpdate datetime)INSERT INTO PromoCalendarState (PromoId, CustomerId, ProductEan, Status, LastUpdateUtc) VALUES (@promoId, @customerId, @productEan, @status, @lastUpdate)
```