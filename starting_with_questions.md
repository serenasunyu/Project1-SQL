Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
```
SELECT DISTINCT city, MAX(totaltransactionrevenue)
FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
AND city != 'not available in demo dataset'
GROUP BY city
LIMIT 1

SELECT DISTINCT country, MAX(totaltransactionrevenue)
FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY country
ORDER BY MAX(totaltransactionrevenue) DESC
LIMIT 1
```

Answer: city - Atlanta, Country - United States


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
```
SELECT DISTINCT als.city, AVG(p.orderedquantity) AS AverageNumProducts
FROM all_sessions als
JOIN products p ON als.productsku = p.sku
GROUP BY als.city


SELECT DISTINCT als.country, AVG(p.orderedquantity) AS AverageNumProducts
FROM all_sessions als
JOIN products p ON als.productsku = p.sku
GROUP BY als.country

Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```
SELECT als.v2productcategory AS CategoryPattern, COUNT(*) AS PatternCount, als.city, als.country
FROM all_sessions als
JOIN products p ON als.productsku = p.sku
WHERE p.orderedquantity > 0
GROUP BY v2productcategory, als.city, als.country
ORDER BY COUNT(*) DESC
```


Answer:
In general, apparel (especially Men's) is ordered the most by customers among all the categories of products. Electronics products, office products, drinkware, and bags are also very popular. (The answer is partly correct because the given product category data is unclear)



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```
With temp as (
	select 
		a.country,
		p.name,
		sum(p.orderedquantity) as totalquantity
	from products p
	left join all_sessions a on p.sku = a.productsku
	group by a.country, 
	p.name
)
select ranked.country, 
		ranked.name, 
		ranked.totalquantity
from (
	select temp.country, 
			temp.name, 
			temp.totalquantity,
			row_number() over (
			partition by temp.country
			order by temp.totalquantity DESC
			) as row_num
	from temp
) as ranked
where row_num = 1


With temp as (
	select 
		a.city,
		p.name,
		sum(p.orderedquantity) as totalquantity
	from products p
	left join all_sessions a on p.sku = a.productsku
	group by a.city, p.name
)
select ranked.city, 
	ranked.name, 
	ranked.totalquantity
from (
	select temp.city, 
		temp.name, 
		temp.totalquantity,
		row_number() over (
			partition by temp.city 
			order by temp.totalquantity DESC
			) as row_num
	from temp
) as ranked
where row_num = 1

```


Answer:
Kick ball, water bottle and custom decals are very popular.


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
-- country
```
SELECT DISTINCT als.country, SUM(anal.revenue) AS TotalRevenue
FROM analytics anal
JOIN all_sessions als ON anal.fullvisitorid = als.fullvisitorid
WHERE anal.revenue IS NOT NULL
GROUP BY als.country
ORDER BY TotalRevenue DESC

-- city

SELECT als.city, SUM(anal.revenue) AS TotalRevenue
FROM analytics anal
JOIN all_sessions als ON anal.fullvisitorid = als.fullvisitorid
WHERE anal.revenue IS NOT NULL
GROUP BY als.city
ORDER BY TotalRevenue DESC

-- or also select country to see where these cities are
```



Answer:
The United States gains the most revenue compared with the other countries. Canada takes the second place.
For product suppliers, they should focus on the North America market more than the others.










