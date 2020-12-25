# Soru 1) 1980’den itibaren spor grubu bazında en çok madalya alan 1. 3. 5. ülkeyi bulalım.

```SQL
select * from (
select Sport,Country,Count(1) AS Count,
ROW_NUMBER() over( PARTITION BY Sport ORDER BY Count(1) DESC) AS Rank from dsmbootcamp.berrin_buyuklu.summer_medals
where Year>=1980
group by Sport,country
order by Sport,Count(1) desc) WHERE Rank IN (1,3,5)
```
