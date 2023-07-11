**What are your risk areas? Identify and describe them.**

The biggest risk exists in the product category column. Because there are many ambiguous values given, such as "Home/Shop by Brand/YouTube/" which does not show the specific category of that product. As a result, when we try to get the category of product sold most, it gives us an ambiguous result, such as "Home/Shop by Brand/YouTube/", "Home/Apparel/Kid's/Kid's-Infant/" and "Home/Apparel/Kid's/Kid's-Infant/" are two different categories.

**QA Process:**
**Describe your QA process and include the SQL queries used to execute it.**

First, write a query to get the categories of products sold.
```
SELECT DISTINCT als.v2productcategory, SUM(p.orderedquantity)
FROM all_sessions als
JOIN products p ON als.productsku = p.sku
WHERE p.orderedquantity > 0
GROUP BY v2productcategory
ORDER BY SUM(p.orderedquantity) DESC
```
I get 71 rows for the different categories and most of them are duplicates. And some of them just give me the sources or mediums through which the visitors made purchases. This means the result I got is not accurate.

Then, maybe it's better to update the productcategory column with accurate values or create a new table with accurate values.
