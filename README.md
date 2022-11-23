## Some SQL queries made by me 

### Link to dump
https://drive.google.com/file/d/1niq7mKEjL3U7RovwvS9Z3xA-fp8mQvRB/view?usp=sharing


**SELECT**


```
SELECT category_id, `name`, AVG(price)
FROM shops.good
GROUP BY `name`
ORDER BY `category_id`;
```

```
SELECT category_id, AVG(price)
FROM shops.good
GROUP BY category_id;
```
```
SELECT id, `name`, email, reg_date
FROM shops.`user`
WHERE reg_date BETWEEN '2018-01-01 00:00:01' AND '2018-01-31 23:59:59'
ORDER BY id;
```

**JOIN**
```
SELECT s.`name`, COUNT(*)
FROM `order_status` s
JOIN `order` o ON s.`id` = o.`status_id`
GROUP BY s.`name`;
```

```
SELECT g.id, g.`name`
FROM  good g
LEFT JOIN shops.order2good o2g ON o2g.good_id = g.id
WHERE o2g.count IS NULL
ORDER BY g.id;
```

```
SELECT u.id, u.`name`
FROM `user` u
JOIN `order` o ON o.id = u.id
JOIN order2good o2g ON o2g.order_id = o.id
JOIN good g ON g.id = o2g.good_id
WHERE g.`name` LIKE '%вечер%'
ORDER BY u.id;
```


**UNION**

```
SELECT o.id, o.creation_date
FROM `order` o
JOIN order_status os ON os.`id` = o.status_id
WHERE os.`code` IN ('NEW', 'APPROVED_BY_STOCK')
UNION
SELECT o.id, o.creation_date
FROM `order` o
JOIN `user` u ON u.id = o.user_id
WHERE u.reg_date BETWEEN '2018-02-01' AND '2018-02-28'
UNION
SELECT o.id, o.creation_date
FROM `order` o
JOIN order2good o2g ON o2g.order_id = o.id
JOIN good g ON g.id = o2g.good_id
WHERE g.`name` LIKE '%йогурт%';
```