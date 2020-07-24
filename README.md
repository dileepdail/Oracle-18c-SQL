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







