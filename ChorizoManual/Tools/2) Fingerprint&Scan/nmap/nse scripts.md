$ cd /usr/share/nmap/scripts 
$ ls | grep -e <keyword>



~samba enumerate users 
nmap --script "smb-enum-users" <IP> 

~vulnerability 
$ nmap -sV --script "vulners" <IP>'" 

~anonymous loging check 

$ nmap --script ftp-anon -p 21 <IP> 

~NFS enumeration
```shell-session
$ sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049
```
