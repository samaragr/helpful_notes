Type: #SQL #commands #cheatsheet #language 

## General 
#general [[SQL - Manipulation]] [[SQL - Data Definition Language (DDL)]]

`*` - allows you to select every column without specifying
`SELECT`  - used to fetch data from a databse (*column name/s*)
	`AS` - rename as an alias (doesnt rename column in table just in return)
	`DISTINCT` - return unique values from specified column
	`WHERE` - use to filter based on condition 
`FROM` - indicates where data is stored i.e. table/database (*table name*) 
`CREATE TABLE` -  Create new table
`CREATE DATABASE` - Create new database
`UPDATE` - edits a row in a table
	`SET` - indicates which ==column== to edit
	`WHERE` - indicates which ==row== to update
	e.g. `UPDATE celebs  
	`SET twitter_handle = '@taylorswift13'`  
	`WHERE id = 4;` (*name = '...' - e.g. alternate indicator*)
`DELETE FROM` - deletes one or more rows (records) form table
	+ use `WHERE` statement to indicate row
	e.g. 
	`DELETE FROM celebs  `
	`WHERE twitter_handle IS NULL;`
		`IS NULL` - returns true if value is NULL 
`NULL` - reps missing or unknown data
`INSERT INTO` - add a record to table, followed by parameter identifying columns that data will be added to
`ALTER TABLE` - make specified changes (*table name*) 
	+ `ADD COLUMN` - adds column to table (*name of column TYPE*)
`ALTER DATABASE` - 
`VALUES` - indicates data being added, parameter identifying values must align with parameter identifying columns under `INSERT` command. Use "" for text etc.
`GROUP BY` - Used with aggregates. Used in collaboration with the `SELECT` statement to arrange identical data into _groups_.
`HAVING` - is a *clause* that allows you to filter which groups (where `WHERE` does rows) to include and which to exclude. Used with aggregates.

## Data types
`INTEGER` - a positive or negative whole number 
`TEXT` - a text string
`DATE` - the date formatted as YYYY-MM-DD
`REAL` - a decimal value

## Constraints
#constraints
`PRIMARY KEY` - columns can be used to uniquely identify the row. Attempts to insert a row with an identical value to a row already in the table will result in a constraint violation which will not allow you to insert the new row
`UNIQUE` - columns have a different value for every row. This is similar to `PRIMARY KEY` except a table can have many different `UNIQUE` columns.
`NOT NULL` - columns must have a value
`DEFAULT` - columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column

## `WHERE` Operators
#operators [[SQL - Querying]]
`=` - equal to
`!` - not equal to
`>` - greater than
`<` - less than
`>=` - greater than or equal to
`<=` - less than or equal to
`LIKE` - search for a similar values
	`_` - a wildcard character
	`%` - matches zero or more missing letters in the pattern e.g. `A%` matches all that begin with letter A, `%a` matches all that end with letter a. Using before and after = "contains" e.g. `%a%`
`NOT` - specify not a value in column
	e.g. `WHERE NOT` *column* = *value*
`IS NULL` - Filters for NULL values
`IS NOT NULL` - Filters out NULL values
`BETWEEN` - filter results with specfied range (*1990 AND 1999*)
`AND` - intersection of two conditions
`OR` - meets either of two conditions
`ORDER BY` - Used to ==sort== *column name*, used after `WHERE`
	`DESC` - descending order (high to low, Z-A)
	`ASC` - ascending order (low to high, A-Z)
`AS` - rename as an alias (doesnt rename column in table just in return)
`DISTINCT` - return unique values from specified column
`LIMIT` - specify max no. of rows results set has. Goes at the end of query
`CASE` - statement allows creation of different outputs (usually in the `SELECT` statement). It is SQL’s way of handling if-then logic. Must end with `END`.
	`WHEN` - tests a condition and the following..
	`THEN` - gives the string if the condition is true
	`ELSE` - gives us the string if all the above conditions are false
	`END` - ends the statement
		+ `AS` - rename column shorter 

## Aggregates
#aggregates [[SQL - Aggregates]] 
`COUNT()` - count the number of rows
`SUM()`- the sum of the values in a column
`MAX()`/`MIN()` - the largest/smallest value
`AVG()` - the average of the values in a column
`ROUND()` - round the values in the column 

## Multiple tables
#multipletables #join [[SQL - Multiple tables]]

`JOIN` - combine information from tables
	`ON` - tells which columns to match rows
`LEFT JOIN` - left join will keep all rows from the first table, regardless of whether there is a matching row in the second table 
`CROSS JOIN` - combine all rows of one table with all rows of another table
`UNION` - Combines two tables with same data
