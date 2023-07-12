# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals

Loading, transforming, cleaning and analyzing data with SQL.

## Process

* Step 1: Load CSV files into pgAdmin4
* Step 2: Transform/clean the data, including changing the format of the data, removing any duplicates in the tables, and so on.
* Step 3: Analyze data according to the questions in part 3 & part 4.
* Step 4: Implement a QA process to validate the transformed data. Find the risk areas and validate them by using queries.
* Step 5: Generate ERD schema to give a clear view of the connections among the tables.

## Results
1. United States has the top sales.
2. Water bottles, custom decals are the top-selling products.
3. Organic search is the main way for customers to make purchases.
4. Customers make their purchases after viewing the first five pages in general.

## Challenge
There are two challenges for me when I was dealing with this data:
1. Unclear column names, such as orderedquantity in products table and total_ordered in sales_report table, productavenue in all_sessions table and avenue in analytics table.
2. It is not easy to assign PK and FK in each table. Because there are no unique values in each column that I can use to set PK in table all_sessions. This may be because more work needs to be done in my data cleaning part.

## Future Goals
what would you do if you had a bit more time?
1. Create new tables to include only columns to be used in the questions.
2. Update v2productcategory values in table all_sessions based on the given productname. In my opinion, the result I get from question 4 in part 3 is not accurate which is generated from the original data.



