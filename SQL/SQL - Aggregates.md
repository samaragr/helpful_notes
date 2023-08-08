Type: #SQL #aggregates

Calculations performed on multiple rows of a table are called **==aggregates==**
follows `SELECT` clause

- `COUNT()` - count the number of rows. A function that takes the name of a column and counts the number of non-empty values in that column
	- e.g.
```sql
SELECT COUNT( * )  
FROM table_name
WHERE price = 0 ;
```

- `SUM()`- the sum of the values in a column
	- e.g.
```sql
SELECT SUM (downloads)
FROM fake_apps;
```

- `MAX()`/`MIN()` - the largest/smallest value
	- `MAX()` - takes the name of a column as an argument and returns the largest value in that column. Here, we returned the largest value in the `downloads` column
	- `MIN()` works the same way but it does the exact opposite; it returns the smallest value
	- e.g.
```sql
SELECT MAX(downloads)
FROM fake_apps;
```

- `AVG()` - the average of the values in a column
	- `AVG()` - function works by taking a column name as an argument and returns the average value for that column
	- e.g.
```sql
SELECT AVG (price)
FROM fake_apps;
```

- `ROUND()` - round the values in the column 
	- By default, SQL tries to be as precise as possible without rounding
	- `ROUND()` - function takes two arguments inside the parenthesis: a column name, and an integer (*specifies dp*)
	- e.g.
```sql
SELECT name, ROUND (price, 0)
FROM fake_apps;
```

```sql
SELECT ROUND(AVG(price),2)
FROM fake_apps;
```

- `GROUP BY` - is a *clause* in SQL that is used with aggregate functions. 
	- It is used in collaboration with the `SELECT` statement to arrange identical data into _groups_.
	- comes after any `WHERE` statements, but before `ORDER BY` or `LIMIT`
	- e.g.
```sql
SELECT category, SUM(downloads)
FROM fake_apps
GROUP BY category;
```

 - e.g.
```sql
SELECT price, COUNT(* ) 
FROM fake_apps  
WHERE downloads > 20000  
GROUP BY price;
```

- SQL lets us use column reference(s) in our `GROUP BY` that will make our lives easier. i.e. `1` is the first column selected
	- e.g.
```sql
SELECT category, price,
AVG(downloads)
FROM fake_apps
GROUP BY 1, 2 

"1 = category and 2 = price"
```


- `HAVING` - is a *clause* that allows you to ==filter which groups== (where `WHERE` does rows) to include and which to exclude. Used with aggregates.
	- `HAVING` - statement always comes after `GROUP BY`, but before `ORDER BY` and `LIMIT`
	- e.g.
```sql
SELECT price,
ROUND(AVG(downloads)),
COUNT(* )
FROM fake_apps
GROUP BY price
HAVING COUNT (* ) >10;
```

 - e.g.
```sql
SELECT location, AVG (employees)
FROM startups
GROUP BY location
HAVING AVG(employees) > 500;
```

