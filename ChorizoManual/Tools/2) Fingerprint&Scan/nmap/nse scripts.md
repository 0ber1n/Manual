$ cd /usr/share/nmap/scripts 
$ ls | grep -e <keyword>



~samba enumerate users 
nmap --script "smb-enum-users" <IP> 

~vulnerability 
$ nmap -sV --script "vulners" <IP>'" 

~anonymous loging check 

$ nmap --script ftp-anon -p 21 <IP> 

