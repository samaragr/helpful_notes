Type: #SQL #DDL  #general #constraints #language 

- `CREATE TABLE` -  Create new table
	- e.g.
```sql
CREATE TABLE person(
id BIGSERIAL NOT NULL PRIMARY KEY,
first_name VARCHAR(50) NOT NULL,
last_name VARCHAR (50) NOT NULL,
date_of_birth DATE NOT NULL,
)
```

- where
	BIGSERIAL - autoincrementing eight-byte integer
	NOT NULL - doesn't allow null values
	PRIMARY KEY - designates primary key

- e.g. 
```sql
CREATE TABLE celebs (  
   id INTEGER,  
   name TEXT,  
   age INTEGER  
);
```

*table_name - name
column_1 data_type - parameter


- `CREATE DATABASE` - Create new database

- `ALTER TABLE` - make specified changes (*table name*) 
	+ `ADD COLUMN` - adds column to table (*name of column TYPE*)
- `ALTER DATABASE` - 
- `DROP` - Delete database/table etc. ==dangerous==
- `TRUNCATE` - 
- `COMMENT` - 
- `RENAME` - 
