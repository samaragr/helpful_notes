INSERTType: #SQL #manipulation  #general #constraints #DML
## Constraints
used to tell the database to reject inserted data that does not adhere to a certain restriction

`PRIMARY KEY` - columns can be used to uniquely identify the row. Attempts to insert a row with an identical value to a row already in the table will result in a constraint violation which will not allow you to insert the new row
`UNIQUE` - columns have a different value for every row. This is similar to `PRIMARY KEY` except a table can have many different `UNIQUE` columns.
`NOT NULL` - columns must have a value
`DEFAULT` - columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column

##  Commands
`*` - allows you to select every column without specifying
`SELECT`  - used to fetch data from a databse (*column name/s*)
	`AS` - rename as an alias (doesnt rename column in table just in return)
	`DISTINCT` - return unique values from specified column
	`WHERE` - use to filter based on condition 
`FROM` - indicates where data is stored i.e. table/database (*table name*)
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
	e.g.
	INSERT INTO person (
	first_name,
	(last_name,
	(date_of_birth)
	VALUES ('Samara', 'Garrett', DATE '1993-11-22')
`VALUES` - indicates data being added, parameter identifying values must align with parameter identifying columns under `INSERT` command. Use "" for text etc.



