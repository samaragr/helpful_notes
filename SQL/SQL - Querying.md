Type: #SQL #querying #operators #case #language 

## SELECT
`SELECT`  - used to fetch data from a databse (*column name/s*). Used everytime you want to query info from a database

## AS
`AS` - rename as an alias (doesnt rename column in table just in return)
e.g.
`SELECT name AS 'Titles'  `
`FROM movies;`

## DISTINCT
`DISTINCT` - return unique values from specified column
e.g.
`SELECT DISTINCT genre  `
`FROM movies;`

## WHERE 

`WHERE` - Used to ==filter== by condition

### Comparison Operators
`=` - equal to
`!=` - not equal to
`>` - greater than
`<` - less than
`>=` - greater than or equal to
`<=` - less than or equal to

### Special operators
`LIKE` - search for a similar values
	e.g.
	`SELECT *   `
	`FROM movies  `
	`WHERE name LIKE 'Se_en';`
		`_` - a wildcard character
		`%` - matches zero or more missing letters in the pattern e.g. `A%` matches all that begin with letter A, `%a` matches all that end with letter a. Using before and after = "contains" e.g. `%a%`
		`!` - not
		`?a%` - second letter is an a
		`'[a-d]%'` - starts with a-d
		`'[acf]%'` - starts with a, c or f
		e.g.
		`SELECT * FROM Customers`
		`WHERE City LIKE '[!acf]%';`
`IS NULL` - Filters for NULL values
`IS NOT NULL` - Filters out NULL values
`BETWEEN` - filter results with specfied range
	e.g.
	`SELECT *  `
	`FROM movies  `
	`WHERE year BETWEEN 1990 AND 1999;`
`AND` - intersection of two conditions
`OR` - meets either of two conditions
`IN` - allows you to specify multiple values in a `WHERE` clause, shorthand for multiple `OR` conditions
	`NOT` - before `IN` 
	e.g.
	`SELECT * FROM Customers `
	`WHERE Country IN ('Norway', 'France');`

## ORDER BY

`ORDER BY` - Used to ==sort== *column name*, used after `WHERE`
	`DESC` - descending order (high to low, Z-A)
	`ASC` - ascending order (low to high, A-Z)

## LIMIT

`LIMIT` - specify max no. of rows results set has. Goes at the end of query

## CASE

`CASE` - statement allows creation of different outputs (usually in the `SELECT` statement). It is SQL’s way of handling if-then logic. ==Must end with== `END`.
	`WHEN` - tests a condition and the following..
	`THEN` - gives the string if the condition is true
	`ELSE` - gives us the string if all the above conditions are false
	`END` - ends the statement
		+ `AS` - rename column shorter 
e.g.
```sql
SELECT name,
CASE
	WHEN genre = 'romance' THEN 'Chill'
	WHEN genre = 'comedy' THEN 'Chill'
	ELSE 'Intense'
	END AS 'Mood'
FROM movies;
```