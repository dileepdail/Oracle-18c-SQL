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
        







