
```sql
WITH RECURSIVE filled_footer AS (SELECT *
                                   FROM footer
                                   WHERE id = (SELECT MIN(id) FROM footer)

                   UNION ALL
   
	SELECT f.id,
           COALESCE(f.car, ff.car) AS car,
           COALESCE(f.length, ff.length) AS length,
           COALESCE(f.width, ff.width) AS width,
           COALESCE(f.height, ff.height) AS height
       FROM footer f
       JOIN filled_footer ff ON f.id = ff.id + 1
     )

SELECT car,
       length,
       width,
       height
	   FROM filled_footer
   ORDER BY id DESC
   LIMIT 1;
```

| car | length | width | height |
|-----|--------|-------|--------|
| Kia Sportage |	12 |	15 |	18 |
