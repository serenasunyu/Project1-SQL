### What issues will you address by cleaning the data?

1. Time is in the format of Unix Timestamp and is not easy to read, same with the visitstarttime;
2. Date needs to be converted into DATE format for the better of future work;
3. There are some duplicates in the analytics table;
4. product price and unit price do not make sense, way too high. 


### Queries:
Below, provide the SQL queries you used to clean your data.

#### TABLE all_sessions

**The format of the time is not clear, converted it to the timestamp for better understanding.**

```
SELECT time, to_timestamp(time)
FROM all_sessions
```


**The data type of the date is an integer, convert it to a date in the format of YYYY-MM-DD.**
**Because the dates are stored as integers with YYYYMMDD, pass it to the date function by first casting to TEXT.**
```
SELECT date(date::TEXT)
FROM all_sessions
```

**Product price does not make sense, based on the cleaning hint, divided by 1,000,000.**

```
SELECT productprice/1000000 AS productprice
FROM all_sessions
```


#### TABLE analytics

**Convert visitstarttime to timestamp.**
```
SELECT visitstarttime, to_timestamp(visitstarttime)
FROM analytics
```

**Convert integer date to date.**
```
SELECT date(date::TEXT)
FROM analytics
```

**Unit_price are divided by 1,000,000.**
```
SELECT unit_price/1000000 AS unit_price
FROM analytics
```


**Delete duplicate row by visitid,date and unit_price.**
```
DELETE FROM analytics
WHERE (visitid, date, unit_price) IN (
  SELECT visitid, date, unit_price
  FROM (
    SELECT visitid, date, unit_price,
           ROW_NUMBER() OVER (PARTITION BY visitid, date, unit_price ORDER BY (SELECT NULL)) AS rn
    FROM analytics
  ) AS subquery
  WHERE rn > 1
);
```

