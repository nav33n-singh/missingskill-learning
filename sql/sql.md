# SQL

* SQL stands for the structured query language.
* It is used to communicate with RDBMS like MYSQL, PostgreSQL, MariaDB, etc.

## Data Types

SQL has 3 basic data types i.e. NUMBER, STRING, DATE and TIME.

### NUMBER

A data-type to store number only. SQL has multiple variants of it, some of them are listed below

1. INT(size): An INTEGER type having signed range from -2147483648 to 2147483647, and unsigned range from 0 to 4294967295. size is display width and ranges from 0 to 255.  
for example, INT(5) ZEROFILL for 377 will be 00377.
2. DEC(size,p): A DECIMAL number with display size and precision.

### STRING

A character string stores characters, numbers and symbols in the form of a string, some of them are  

1. CHAR(size): A fixed-length string with length ranging from 0 to 255, default length is 1. Here size indicates the length of the string.  
for example: for CHAR(4) 'a' will be stored like 'a___', here _ represents space, and  
'abcdefgh' will be stored like 'abcd' in **not restrict SQL mode** and in **restrict SQL mode** it will get discarded.

1. VARCHAR(size): A variable-length string with a length ranging from 0 to 65535.  
for example: for VARCHAR(10) 'a' will be stored like 'a' only.  

| Value      | CHAR(4) | Storage Required | VARCHAR(4) | Storage Required |
| ---------- | ------- | ---------------- | ---------- | ---------------- |
| ''         | '____'  | 4 bytes          | ''         | 1 byte           |
| 'ab'       | 'ab__'  | 4 bytes          | 'ab'       | 3 bytes          |
| 'abcd'     | 'abcd'  | 4 bytes          | 'abcd'     | 5 bytes          |
| 'abcdefgh' | 'abcd'  | 4 bytes          | 'abcd'     | 5 bytes          |

_NOTE:_ represents space in table_

### DATE and TIME

1. DATE: Stores date in format 'YYYY-MM-DD'
2. TIME: Stores time in the format 'hh:mm:ss'
3. YEAR Stores year in format 'YYYY'
4. TIMESTAMP: Stores time stamp in the format 'YYYY_MM_DD hh:mm:ss'

## CONSTRAINTS

Constraints add extra properties to fields.

| Constraints | Description                                                            |
|-------------|------------------------------------------------------------------------|
| NOT NULL    | Ensures that column so not receive an empty value                      |
| UNIQUE      | Ensures uniqueness of all values in column                             |
| PRIMARY KEY | An UNIQUE and NOT NULL field used to identify rows in a table uniquely |
| FOREIGN KEY | A field in one table that refers to the primary key on another table   |
| DEFAULT     | Sets a default value to the column if no value passed                  |
| CHECK       | Checks if input satisfies the specified condition in a column          |

## RDBMS

* It stands for Relational Database Model System.
* Relational databases store data in databases in the form of tables.
* Tables are made up of rows and columns.
* Columns are also knowns as properties and rows are known as records.
* MySQL,PostgreSQL,MariaDB,MSSQL are some examples of RDBMS.