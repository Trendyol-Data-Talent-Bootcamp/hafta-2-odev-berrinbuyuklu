# Soru 4)

```SQL
MERGE berrin_buyuklu.content_category T
USING berrin_buyuklu.content_category_20201222_00_59 S
ON T.id = S.id
WHEN MATCHED THEN
  UPDATE SET T.cdc_date = S.cdc_date, T.is_deleted = S.is_deleted, T.category = S.category 
WHEN NOT MATCHED BY SOURCE THEN
  UPDATE SET T.is_deleted = true
WHEN NOT MATCHED BY TARGET THEN
  INSERT (cdc_date,is_deleted,id,category) VALUES (S.cdc_date,S.is_deleted,S.id,S.category);
```

Kontrol için

```SQL
select farm_fingerprint(to_json_string(t1)) = farm_fingerprint(to_json_string(t2)) as is_equal,
COUNT(1) as count from 
`berrin_buyuklu.content_category_target` t1 FULL OUTER JOIN berrin_buyuklu.content_category t2 ON t1.id = t2.id
GROUP BY is_equal;
```
