Tip: use the flag -ic to skip the comment lines of a wordlist.

Standard syntax:

```cli
ffuf -w /wordlist.txt:FUZZ -u http://domain/FUZZ
```

#### Page Fuzzing
```
ffuf -w /wordlis.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v
```

#### Subdomain Fuzzing

Good subdomain wordlist: 
```
seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

Subdomain syntax:
```
ffuf -w /wordlis.txt:FUZZ -u http://FUZZ.SERVER_IP:PORT/
```

#### Vhost Fuzzing

Good vhost wordlist:
```
seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

vhost syntax:
```
ffuf -w /wordlist.txt:FUZZ -u http://BASE_DOMAIN/ -H 'Host: FUZZ.BASE_DOMAIN'
```


#### Parameter Fuzzing

Good parameter wordlist:
```
seclists/Discovery/Web-Content/burp-parameter-names.txt
```

Fuzz for GET requests:
```
ffuf -w wordlist.txt:FUZZ -u http://DOMAIN/admin.php?FUZZ=key -fs xxx
```

Fuzz with POSTS requests:
```
ffuf -w wordlist.txt:FUZZ -u http://DOMAIN/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx
```

#### User Enumeration With Web Login Form
Good user wordlist:
```
seclists/Usernames/xato-net-10-million-usernames.txt
```

Username Fuzz with GET:
```
ffuf -w /wordlist.txt -u http://1DOMAIN/index.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "username=FUZZ&password=invalid" -fr "Unknown user(Error Message)"
```

#### Fuzzing with phpsessionID
This can be used for things like password resets.

```
ffuf -w ./city_wordlist.txt -u http://DOMAIN/security_question.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -b "PHPSESSID=enter_ID_here" -d "security_response=FUZZ" -fr "Incorrect response."
```

#### Login Clusterbomb

```
ffuf -request req.txt -request-proto http -mode clusterbomb -w /path/to/usernames.txt:FUZZUSER -w /path/to/passwords.txt:FUZZPASS -mc Wanted_status
```
