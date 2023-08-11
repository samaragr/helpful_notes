Type: #SQL #multipletables #join #language 

- ==Primary key== - a column that uniquely identifies each row of that table
	-   None of the values can be `NULL`.
	-   Each value must be unique (i.e., you can’t have two customers with the same `customer_id` in the `customers` table).
	-   A table can not have more than one primary key column.

- ==Foreign key== - When the primary key for one table appears in a different table

`JOIN` - combine information from tables (*aka inner join*), deletes rows without matching info 
	`ON` - tells which columns to match rows
	e.g.
	`SELECT *`
	`FROM orders` -- table 1
	`JOIN customers` -- table 2
	`ON orders.customer_id`
	`= customers.customer_id;`
	The fourth line tells us how to combine the two tables. We want to match `orders` table’s `customer_id` column with `customers` table’s `customer_id` column.
	e.g.
	`SELECT *`
	`FROM orders`
	`JOIN subscriptions`
	`ON orders.subscription_id`
	`= subscriptions.subscription_id`
	`WHERE subscriptions.description = 'Fashion Magazine';`

`LEFT JOIN` - left join will keep all rows from the first table, regardless of whether there is a matching row in the second table 
	e.g.
	`SELECT *`
	`FROM newspaper`
	`LEFT JOIN online`
	`ON newspaper.id = online.id`
	`WHERE online.id IS NULL;`

`CROSS JOIN` - combine all rows of one table with all rows of another table aka all possible combinations
	e.g.
	`SELECT *`
	`FROM newspaper`
	`CROSS JOIN months`
	`WHERE start_month <= month`
	`AND end_month >= month`
	`GROUP BY month;`

`UNION` - Combines two tables with same data
	-   Tables must have the same number of columns.
	-   The columns must have the same data types in the same order as the first table.
	- e.g.
	`SELECT *`
	`FROM newspaper`
	`UNION`
	`SELECT *`
	`FROM online;`

`WITH` - statement allows us to perform a separate query (such as aggregating customer’s subscriptions)
	use an alias to contain a query, then run a second query on the alias
	e.g.
```sql
WITH previous_query AS ( 
	SELECT customer_id, 
	COUNT(subscription_id) AS 'subscriptions' 
	FROM orders  
	GROUP BY customer_id 
	) 
SELECT customers.customer_name,
previous_query.subscriptions 
FROM previous_query 
JOIN customers 
ON previous_query.customer_id = customers.customer_id;
```

`FULL JOIN` - (*FULL OUTER JOIN*) returns all rows from both tables

