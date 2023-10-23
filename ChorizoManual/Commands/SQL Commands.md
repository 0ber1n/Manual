- SELECT - retrieve data from a database 
    
- INSERT - insert data into a database 
    
- UPDATE - updates existing data within a database 
    
- DELETE - delete records from a database 
    
- Example: 
    
    Retrieve data: 
    SELECT phone  FROM employees 
    WHERE userid = 96134; 
    This statement retrieves the phone number of the employee who has the userid 96134. 
    

Update data: 

UPDATE Customers 
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt' 
WHERE CustomerID = 1; 
***********************************************************

DDL commands are used for creating, modifying, and dropping the structure of database objects. 

- CREATE - create database objects such as tables and views 
    
- ALTER - alters the structure of the existing database 
    
- DROP - delete objects from the database 
    
- Example: 
    
    - CREATE TABLE employees(     userid varchar(6) not null primary key,     first_name varchar(20),     last_name varchar(20),     department varchar(20),     salary varchar(10),     auth_tan varchar(6) ); 
        
    - This statement creates the employees example table given on page 2. 
        

Adding columns to the table: 

ALTER TABLE table_name 
ADD column_name datatype; 
DROP TABLE Shippers; 

******************************************************

Data Control Language (DCL) commands are used to implement access control on database objects. 

- GRANT - give a user access privileges on database objects 
    
- REVOKE - withdraw user privileges that were previously given using GRANT 
    

EX:  GRANT ALL ON table_name To username/roleAL 

Special Characters 

/* */          are inline comments -- , #          are line comments  

Example: SELECT * FROM users WHERE name = 'admin' -- AND pass = 'pass' 

;        allows query chaining  

Example: SELECT * FROM users; DROP TABLE users; 

',+,||         allows string concatenation Char()         strings without quotes  

Example: SELECT * FROM users WHERE name = '+char(27) OR 1=1 

Special Statements 

Union 

The Union operator is used, to combine the results of two or more SELECT Statements. 

Rules to keep in mind, when working with a UNION: 

- The number of columns selected in each statement must be the same. 
    
- The datatype of the first column in the first SELECT statement, must match the datatype of the first column in the second (third, fourth, …​) SELECT Statement. The Same applies to all other columns. 
    

SELECT first_name FROM user_system_data UNION SELECT login_count FROM user_data; 

The UNION ALL Syntax also allows duplicate Values 

. 

Joins 

The Join operator is used to combine rows from two or more tables, based on a related column 

SELECT * FROM user_data INNER JOIN user_data_tan ON user_data.userid=user_data_tan.userid;