~numerate smb shares on 445 TCP 
$ smbclient -L <IP> 

~Connect to each share (watch double slashes) 
$ smbclient \\\\<IP> \\<SHARENAME>-U Administrator   (hit enter on password) 

$ smbclient -N -L [\\\\{TARGET_IP}\\](file:///\\\\{TARGET_IP}\\)
-N : No password -L : This option allows you to look at what services are available on a server