# Oracle-18c-SQL
Oracle SQL Basic Queries and Concepts

###### Download Oracle Database Express Edition (XE)
Link: https://www.oracle.com/database/technologies/xe-downloads.html  
*Check on Oracle Website

###### Download Oracle SQL Developer
Link: https://www.oracle.com/tools/downloads/sqldev-v192-downloads.html  
*Check on Oracle Website

###### Create New Connetion in Oracle SQL Developer
1. Enter Connection Name
2. Enter User: SYS
3. Enter Pass: ********
4. Hostname: localhost(or IP)
5. Port: 1521
6. Service Name: XEPDB1
7. Click Test to check the connection. You should see success msg.
8. Click Connect. Enter Password

###### Create new User in DB

    CREATE USER intro_user IDENTIFIED BY mypassword;

    GRANT CONNECT TO intro_user;

    GRANT CREATE SESSION, GRANT ANY PRIVILEGE TO intro_user;

    GRANT UNLIMITED TABLESPACE TO intro_user;

    GRANT CREATE TABLE TO intro_user;
    
*Create New DB connection using new user 'intro_user'

## View Queries(Data)

    --Select all records from Table
    select * from employee;

    --Filter using WHERE
    select first_name from employee;

    --Comparison operator
    select * from employee where salary > 1000;

    select * from employee where salary <> 1000;

    select * from employee where salary = 51000;

    --Like syntax

    select * from employee where first_name like '%ry';

    select * from employee where first_name like '%ry%';

    select * from employee where first_name like 'A%';

    select * from employee where first_name like 'Ada_';

    select * from employee where first_name like '_dam';

    --Filtering on Date Values

    --check db date format
    select value from SYS.nls_database_parameters
    where parameter = 'NLS_DATE_FORMAT';

    select * from employee where hire_date = '03-OCT-2010';

    select * from employee where hire_date = '03-OCT-2010';

    --Two Filters using OR & AND

    select * from employee
    where first_name = 'Ann'
    and last_name = 'Bowman';

    select * from employee
    where first_name = 'Ann'
    or last_name = 'Bowman';

    --More than two filters. Use () to be specific about OR & AND
    --AND takes priority over OR

    select * from employee
    where (first_name = 'Ann'
    AND last_name = 'Bowman')
    OR salary > 20000;


    select * from employee
    where first_name = 'Ann'
    AND (last_name = 'Bowman'
    OR salary > 20000);


    select * from employee
    where first_name = 'Ann'
    AND (last_name = 'Bowman'
    OR salary > 20000);

    --NULL

    select * from employee
    where salary IS NULL;

    select * from employee
    where salary IS NOT NULL;

    --Unique result with DISTINCT

    select DISTINCT last_name from employee;

    select DISTINCT last_name, department_id from employee;
    
    --IN and NOT IN

    select * from employee
    where last_name ='Berry'
    OR last_name ='Foster'
    OR last_name ='Powell'
    OR last_name ='Burns'
    OR last_name ='Jones';

    select * from employee
    where last_name IN('Berry','Foster','Powell','Burns','Jones');

    select * from employee
    where last_name NOT IN ('Berry','Foster','Powell','Burns','Jones');

    --BETWEEN and NOT BETWEEN

    select * from employee
    where salary
    BETWEEN 100000 AND 200000;

    select * from employee
    where hire_date
    BETWEEN '15-NOV-15'
    AND '17-JUL-16';

    select * from employee
    where hire_date
    NOT BETWEEN '15-NOV-10'
    AND '17-JUL-16';

    --ALL keyword
    --Oposite to IN which uses OR comparison in values
    --ALL uses AND in all values

    select * from employee
    where salary < ALL(30000,40000,50000);

    select * from employee
    where salary = ALL(30000);


    --ANY keyword
    --column = ANY() Column needs to match at least one of the values in the list

    select * from employee
    where salary = ANY(30000,40000,50000);
    
    
## Sorting Data

    select * from employee
    ORDER BY first_name;
    --Is same as
    select * from employee
    ORDER BY first_name ASC;

    select * from employee
    ORDER BY first_name DESC;

    --Ordering by multiple columns

    select * from employee
    ORDER BY first_name ASC,
    employee_id DESC;
    
## Set Operators

###### UNION: 
*Combines the result of two sets and removes duplicate records.
*The number of column in both quesries should be the same.

    select first_name, last_name 
    from employee
    UNION
    select first_name, last_name 
    from customer;
    
    select 'Employee', first_name, last_name 
    from employee
    UNION
    select 'Customer', first_name, last_name 
    from customer;
    
###### UNION ALL: 
*Combines the result of two sets and keep duplicate records.

    select first_name, last_name 
    from employee
    UNION ALL
    select first_name, last_name 
    from customer;
    
###### INTERSECT:
*Return results that appear in both queries.

    select first_name, last_name 
    from employee
    INTERSECT
    select first_name, last_name 
    from customer;
    
###### MINUS:
*Return result of query 1 minus query 2.

    select first_name, last_name 
    from employee
    MINUS
    select first_name, last_name 
    from customer;
    
###### Three or more Sets in single query

    select * from employee
    where salary
    BETWEEN 10000 AND 30000
    UNION
    select * from employee
    where salary
    BETWEEN 30000 AND 40000
    UNION
    select * from employee
    where salary
    BETWEEN 40000 AND 50000
    
    
    select * from employee
    where salary
    BETWEEN 10000 AND 30000
    UNION
    select * from employee
    where salary
    BETWEEN 30000 AND 40000
    INTERSECT
    select * from employee
    where salary
    BETWEEN 40000 AND 50000
    
 ## Aggregate Functions and Grouping
 
 ###### Counting Data
    
    --Total number of record in table
    select count(*) from employee;
    
    --Exclude the null value of column
    select count(salary) from employee;

    select count(DISTINCT first_name) from employee;
    
###### Conting Data within groups with GROUP BY

    -- The select column and GROUP BY should be same
    select last_name, count(*) 
    from employee
    GROUP BY last_name;
    
###### GROUP BY with WHERE and ORDER BY

    -- First WHERE then GROUP BY and then ORDER BY
    select last_name, count(*) 
    from employee
    where last_name LIKE 'B%'
    GROUP BY last_name
    ORDER BY COUNT(*) DESC;

    select last_name, count(*) 
    from employee
    where last_name LIKE 'B%'
    GROUP BY last_name
    ORDER BY last_name;
    
###### GROUP BY with Multiple Columns

    select last_name, department_id, count(*) 
    from employee
    GROUP BY last_name, department_id;
    
###### GROUP BY with HAVING

    select last_name, count(*) 
    from employee
    GROUP BY last_name
    HAVING count(*) > 1;
    
    select last_name, count(*) 
    from employee
    GROUP BY last_name
    HAVING last_name like 'B%';
    
###### The SUM Function

    select SUM(salary) 
    from employee;

    select department_id, SUM(salary) 
    from employee
    GROUP BY department_id;
    
###### Using the MAX and MIN functions

    select MAX(salary) 
    from employee;

    select MAX(salary), MIN(salary) 
    from employee;

    select department_id, MAX(salary) 
    from employee
    GROUP BY department_id;
    
###### Using the AVG function

    select AVG(salary) 
    from employee;
    

## Joins

###### Table Aliases
*Aliases = shorter names for tables

    select e.department_id 
    from employee e;
    
###### Column Aliases

    select count(*) AS no_of_employee from employee;
    
###### What are joins
*Query from two tables at once, linked using a common value

1. Inner Join: Linked two tables based on a common value.

        SELECT e.employee_id,
        e.first_name,
        e.salary,
        d.department_name,
        d.department_id
        FROM employee e
        JOIN department d
        ON e.department_id = d.department_id
        WHERE e.salary > 400000;
    
2. Left Outer Join: Include all value from table 1 and include matching value or NULL from table 2

        SELECT c.customer_id,
        c.first_name,
        c.last_name,
        co.order_date,
        d.department_id
        FROM customer c
        LEFT JOIN customer_order co
        ON c.customer_id = co.customer_id;
    
3. Right Outer Join: Include all value from table 2 and include matching value or NULL from table 1

        SELECT c.customer_id,
        c.first_name,
        c.last_name,
        co.order_date,
        d.department_id
        FROM customer c
        RIGHT JOIN customer_order co
        ON c.customer_id = co.customer_id;
    
4. Full Outer Join: Combination of Left joins and Right joins

        SELECT c.customer_id,
        c.first_name,
        c.last_name,
        co.order_date,
        d.department_id
        FROM customer c
        FULL JOIN customer_order co
        ON c.customer_id = co.customer_id;
    
5. Natural Join: Two tables joined on columns that have the same names
*Node need to specify the columns

        --All the columns are same in both tables
        SELECT product_id,
        product_name,
        department_id,
        department_name
        FROM product
        NATURAL JOIN department;
    
        --With partial common column
        SELECT e.employee_id,
        e.first_name,
        e.last_name,
        department_id, --common column
        d.department_name
        FROM employee e
        NATURAL JOIN department d;
    
5. Cartesian or Cross Join: Every record in one table is joined to every record in another table
        
        SELECT employee_id,
        first_name,
        last_name,
        department_name
        FROM employee, department;
    
6. Self Join: Join a table to itself. Used when a record in a table is related to another record in the same table

        SELECT emp.employee_id,
        emp.first_name,
        emp.last_name,
        emp.manager_id,
        mgr.first_name,
        mgr.last_name
        FROM employee emp
        LEFT JOIN emploee mgr 
        ON emp.manager_id=mgr.employee_id;
        
        
## Functions

###### String Functions

*Eg. LENGTH(first_name): Returns the length of the value

###### Nested Functions

*Eg. SUBSTR(email_address, INSTR(email_address, '@'), LENGTH(email_address))

###### Number Functions

*Eg. Price: 149.95

1. ROUND: Rounds the nearest whole number or specified decimal places
*ROUND(price)
*Output: 150

2. FLOOR: Rounds down the nearest whole number
*FLOO(price)
*Output: 149

3. CEIL: Rounds up the nearest whole number
*CEIL(price)
*Output: 150

###### Date Functions

1. SYSYDATE: current date

        SELECT employee_id,
        SYSDATE
        FROM employee;

2. ADD_MONTHS: Adds a number of months to a date value

        SELECT employee_id,
        SYSDATE,
        ADD_MONTHS(hire_date, 6) AS review_date
        FROM employee;

3. MONTHS_BETWEEN: Finds the diffrence between two date values

        SELECT employee_id,
        SYSDATE AS curr_date,
        ADD_MONTHS(hire_date, 6) AS review_date,
        MONTHS_BETWEEN(hire_date, SYSDATE) AS time_with_company
        FROM employee;
        
###### Data Types and Conversion Functions

*Broadly: String Types, NUmber Types, or Date Types

Common Data Types:

1. CHAR: Character String with fixed size

2. VARCHAR2: Character String with variable size

3. NUMBER: Stores numeric data with optional decimals

4. DATE: Stores date and time

5. TIMESTAMP: Stores date, time, and fractional seconds

6. CLOB: Stores large amount of text.

Convrting:

1. TO_CHAR: Converts a DATE or INTERVAL value to a string in a specified date format 
        
        SELECT employee_id,
        hire_date,
        TO_CHAR(hire_date, 'YYYY_MM_DD')
        FROM employee;
        
2. TO_DATE: Converts a string to a date.

        SELECT TO_DATE('2017_05_28','YYYY_MM_DD')
        FROM dual;

3. TO_NUMBER: Converts a string to a number.

        SELECT TO_NUMBER('200')
        FROM dual;
        
###### The CASE Statement

*Perform conditional login in SQL
*IF THEN ELSE

        SELECT product_id,
        product_name,
        price,
        CASE
        WHEN price > 100 THEN 'Over 100'
        WHEN price < 100 THEN 'Less than 100'
        ELSE '100'
        END price_group
        FROM product;


## Inserting, Updating, and Deleting Data

###### Inserting Data

    INSERT INTO table
    (column1, column2, ... )
    VALUES
    (expression1, expression2, ... );
    
    INSERT ALL
    INTO table (column1, column2, ... ) VALUES (expression1, expression2, ... )
    INTO table (column1, column2, ... ) VALUES (expression1, expression2, ... )
    INTO table (column1, column2, ... ) VALUES (expression1, expression2, ... );
    
###### Inserting Data From Another Table

    INSERT INTO table
    (column1, column2, ... )
    SELECT expression1, expression2, ...
    FROM source_tables
    [WHERE conditions];
    
###### Updating Data

    UPDATE employee
    SET salary=800000
    WHERE employee_id=55;
    
    UPDATE employee
    SET salary=slary+20000
    WHERE employee_id=55;
    
###### Deleting Data

    DELETE from employee
    WHERE employee_id=55;
    
###### COMMIT and ROLLBACK

    COMMIT;
    ROLLBACK;
    
###### Truncating Data

Removes data from table  
Simlar to DELETE with no WHERE condition  
*NO ROLL BACK allowed

    TRUNCATE table customer_order;
    

## Creating, Altering, and Dropping Tables

###### DML: Data Manipuation Language

*Statemets that change or manipulate data

1. SELECT
2. INSERT
3. UPDATE
5. DELETE

###### DDL: Data Definition Language

*Statemets that define objects, such as table

###### CREATE Table

    CREATE TABLE customers
    ( customer_id number(10) NOT NULL,
      customer_name varchar2(50) NOT NULL,
      city varchar2(50)
    );
    
###### ALTER a Table

    ALTER TABLE employee
    ADD job_description VARCHAR2(200);
    
    ALTER TABLE employee
    DROP COLUMN job_description;
    
    ALTER TABLE employee
    RENAME COLUMN job_description TO job_details;
    
    ALTER TABLE job_role
    RENAME TO job_title;
    
###### DROP a Table

    DROP TABLE job_role
    
    
*Reference: Oracle SQL - A Complete Introduction By Ben Brumm
