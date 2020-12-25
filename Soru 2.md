# Soru 2) 1980’den itibaren herhangi bir spor grubunda üst üste 3 veya daha fazla madalya almış atletleri bulalım.

```SQL
SELECT *
from (
select Sport,Athlete,Year ,
(COUNT(Year) OVER(PARTITION BY Sport,Athlete ORDER BY Sport,Athlete,Year ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)) as GroupCount,
(MAX(Year) OVER(PARTITION BY Sport,Athlete ORDER BY Sport,Athlete,Year ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)) as GroupMaxYear,
(MIN(Year) OVER(PARTITION BY Sport,Athlete ORDER BY Sport,Athlete,Year ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)) as GroupMinYear,
from dsmbootcamp.berrin_buyuklu.summer_medals
where Year>=1980
group by Sport,Athlete,Year
order by Sport,Athlete,Year) 
WHERE GroupCount = 3 AND GroupMaxYear-GroupMinYear = 8;
```
