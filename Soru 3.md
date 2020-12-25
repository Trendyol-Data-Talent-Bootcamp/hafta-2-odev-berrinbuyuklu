# Soru 3) "sample.pageview": tablosunda 1 gün içerisinde trendyol.com a gelen tüm ziyaretlerin logu var.

```SQL
select view_period,
(SUM(active_user_count) OVER(ORDER BY view_period ROWS BETWEEN 4 PRECEDING AND 0 FOLLOWING)) as active_user 
FROM 
(select timestamp_trunc(view_ts,minute) view_period,
count(distinct deviceid) active_user_count
from berrin_buyuklu.pageview
GROUP BY timestamp_trunc(view_ts,minute))
```
