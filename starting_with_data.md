Question 1: What is the average number of pages viewed by the visitors?

SQL Queries:
```
SELECT AVG(pageviews)
FROM all_sessions
``

Answer:
4.5248447204968944



Question 2: What is the most frequent channel for visitors to make orders? 

SQL Queries:
```
SELECT als.channelgrouping,COUNT(*)
FROM all_sessions als
JOIN sales_report sr ON als.productsku = sr.productsku
WHERE total_ordered > 0
GROUP BY als.channelgrouping
ORDER BY COUNT(*) DESC
```

Answer:
Organic Search



Question 3: What product/products do not have enough stock?

SQL Queries:
```
SELECT name, orderedquantity, stocklevel
FROM products
WHERE orderedquantity > stocklevel
```

Answer:
15 rows


Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
