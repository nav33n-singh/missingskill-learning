## MySQL

## CRUD

It stands for Create, Read, Update and Delete. These are some basic operations on an RDBMS.

* Create

Can be used to create a database, table, view, procedures, here we will concentrate on databases and tables.  

1. Creating a database

```sql
SHOW DATABASES; -- list all databases
USE databaseName; -- to select a database
DROP DATABASE databaseName; -- Deletes database


CREATE DATABASE ACADEMY; --creates a database named ACADEMY
```

2. Creating a table

```sql
    CREATE TABLE students(
        student_ID INT NOT NULL AUTO_INCREMENT,
        fname VARCHAR(30) NOT NULL,
        lname VARCHAR(20) NOT NULL,
        dob DATE,
        PRIMARY KEY(student_ID)
        );
```  

Inserting values into tables

```sql
    INSERT INTO students VALUES(1,'John','Wick','1994-05-01');
    INSERT INTO students(fname,lname,dob) VALUES
    ('Josh','jackson','1994-02-21'),
    ('Alan','Walker','1993-03-30'),
    ('Ajay','Ghale','1995-06-26'),
    ('Naveen','Singh','1994-04-24');
```

* READ

Reading data from table

```sql
SELECT * FROM students;

+------------+--------+---------+------------+
| student_ID | fname  | lname   | dob        |
+------------+--------+---------+------------+
|          1 | John   | Wick    | 1994-05-01 |
|          2 | Josh   | jackson | 1994-02-21 |
|          3 | Alan   | Walker  | 1993-03-30 |
|          4 | Ajay   | Ghale   | 1995-06-26 |
|          5 | Naveen | Singh   | 1994-04-24 |
+------------+--------+---------+------------+


SELECT student_ID FROM students WHERE fname = 'John';

+------------+
| student_ID |
+------------+
|          1 |
+------------+

```

* UPDATE

Updating existing data in the table

```sql
    UPDATE students
    SET fname = 'Joseph'
    WHERE student_ID = 2;
+------------+--------+---------+------------+
| student_ID | fname  | lname   | dob        |
+------------+--------+---------+------------+
|          1 | John   | Wick    | 1994-05-01 |
|          2 | Joseph | jackson | 1994-02-21 |
|          3 | Alan   | Walker  | 1993-03-30 |
|          4 | Ajay   | Ghale   | 1995-06-26 |
|          5 | Naveen | Singh   | 1994-04-24 |
+------------+--------+---------+------------+
```

Alter: Used to ADD, DROP or MODIFY table in a database.

```sql

--adding a column in students
ALTER TABLE students
ADD email VARCHAR(50);

SELECT * FROM students;
+------------+--------+---------+------------+-------+
| student_ID | fname  | lname   | dob        | email |
+------------+--------+---------+------------+-------+
|          1 | John   | Wick    | 1994-05-01 | NULL  |
|          2 | Joseph | jackson | 1994-02-21 | NULL  |
|          3 | Alan   | Walker  | 1993-03-30 | NULL  |
|          4 | Ajay   | Ghale   | 1995-06-26 | NULL  |
|          5 | Naveen | Singh   | 1994-04-24 | NULL  |
+------------+--------+---------+------------+-------+

UPDATE students 
SET email = CONCAT(fname,lname,'@academy.edu')
+------------+--------+---------+------------+---------------------------+
| student_ID | fname  | lname   | dob        | email                     |
+------------+--------+---------+------------+---------------------------+
|          1 | John   | Wick    | 1994-05-01 | JohnWick@academy.edu      |
|          2 | Joseph | jackson | 1994-02-21 | Josephjackson@academy.edu |
|          3 | Alan   | Walker  | 1993-03-30 | AlanWalker@academy.edu    |
|          4 | Ajay   | Ghale   | 1995-06-26 | AjayGhale@academy.edu     |
|          5 | Naveen | Singh   | 1994-04-24 | NaveenSingh@academy.edu   |
+------------+--------+---------+------------+---------------------------+


--modifying a column in students  

ALTER TABLE students
MODIFY email VARCHAR(50) NOT NULL;

--deleting a column in students

ALTER TABLE students
DROP COLUMN email;

select * from  students;
+------------+--------+---------+------------+
| student_ID | fname  | lname   | dob        |
+------------+--------+---------+------------+
|          1 | John   | Wick    | 1994-05-01 |
|          2 | Joseph | jackson | 1994-02-21 |
|          3 | Alan   | Walker  | 1993-03-30 |
|          4 | Ajay   | Ghale   | 1995-06-26 |
|          5 | Naveen | Singh   | 1994-04-24 |
+------------+--------+---------+------------+
```

* DELETE

Used to delete data from the table.

```sql
--To delete specific records
    DELETE FROM students
    WHERE fname = 'John';

    select * from students;
+------------+--------+---------+------------+
| student_ID | fname  | lname   | dob        |
+------------+--------+---------+------------+
|          2 | Joseph | jackson | 1994-02-21 |
|          3 | Alan   | Walker  | 1993-03-30 |
|          4 | Ajay   | Ghale   | 1995-06-26 |
|          5 | Naveen | Singh   | 1994-04-24 |
+------------+--------+---------+------------+

--to delete everything from the table

DELETE FROM students;
SELECT * FROM students;
--o/p Empty set (0.00 sec)
```

## UNION

* Combines results from multiple SELECT statements.
* Number of columns must be the same.
* Data types of columns must be the same.
* Order in the select statement must be the same.

```sql
--UNION //rejects duplicate records
    SELECT super_id FROM employee
    UNION
    SELECT mgr_id FROM branch;
+----------+
| super_id |
+----------+
|     NULL |
|      100 |
|      102 |
|      106 |
+----------+


--UNION ALL //shows duplicate records also

    SELECT super_id FROM employee
    UNION ALL
    SELECT mgr_id FROM branch;

    +----------+
| super_id |
+----------+
|     NULL |
|      100 |
|      100 |
|      100 |
|      102 |
|      102 |
|      102 |
|      106 |
|      106 |
|      100 |
|      102 |
|      106 |
+----------+
```

## JOINS

Used to combine rows of multiple tables having related columns.

1. Inner JOIN: Selects intersection of both select statements.

```sql
    SELECT employee.first_name,employee.salary,branch.branch_name
    FROM employee
    JOIN branch
    WHERE employee.emp_id = branch.mgr_id;
+------------+--------+-------------+
| first_name | salary | branch_name |
+------------+--------+-------------+
| David      | 250000 | Corporate   |
| Michael    |  75000 | Scranton    |
| Josh       |  78000 | Stamford    |
+------------+--------+-------------+
```

2. LEFT JOIN: Selects everything from the left table and shows corresponding values of the right table

```sql
    SELECT employee.first_name,employee.salary,branch.branch_name
    FROM employee
    LEFT JOIN branch ON
    employee.emp_id = branch.mgr_id;
+------------+--------+-------------+
| first_name | salary | branch_name |
+------------+--------+-------------+
| David      | 250000 | Corporate   |
| Jan        | 110000 | NULL        |
| Michael    |  75000 | Scranton    |
| Angela     |  63000 | NULL        |
| Kelly      |  55000 | NULL        |
| Stanley    |  69000 | NULL        |
| Josh       |  78000 | Stamford    |
| Andy       |  65000 | NULL        |
| Jim        |  71000 | NULL        |
+------------+--------+-------------+
```

3. RIGHT JOIN: Selects everything from the right table and show corresponding values from the left table

```sql
    SELECT employee.first_name,employee.salary,branch.branch_name
    FROM employee
    RIGHT JOIN branch ON
    employee.emp_id = branch.mgr_id;
+------------+--------+-------------+
| first_name | salary | branch_name |
+------------+--------+-------------+
| David      | 250000 | Corporate   |
| Michael    |  75000 | Scranton    |
| Josh       |  78000 | Stamford    |
+------------+--------+-------------+
```

4. FULL JOIN: LEFT JOIN UNION RIGHT JOIN

```sql
    SELECT employee.first_name,employee.salary,branch.branch_name
    FROM employee
    LEFT JOIN branch ON
    employee.emp_id = branch.mgr_id
    UNION ALL
    SELECT employee.first_name,employee.salary,branch.branch_name
    FROM employee
    RIGHT JOIN branch ON
    employee.emp_id = branch.mgr_id;

+------------+--------+-------------+
| first_name | salary | branch_name |
+------------+--------+-------------+
| David      | 250000 | Corporate   |
| Jan        | 110000 | NULL        |
| Michael    |  75000 | Scranton    |
| Angela     |  63000 | NULL        |
| Kelly      |  55000 | NULL        |
| Stanley    |  69000 | NULL        |
| Josh       |  78000 | Stamford    |
| Andy       |  65000 | NULL        |
| Jim        |  71000 | NULL        |
| David      | 250000 | Corporate   |
| Michael    |  75000 | Scranton    |
| Josh       |  78000 | Stamford    |
+------------+--------+-------------+
```


