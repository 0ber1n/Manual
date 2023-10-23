~Update /etc/hosts file with new host
$ echo "10.129.43.181  unika.htb" | sudo tee -a /etc/hosts 

~append to end of host file list 
$ echo "IP_ADDRESS [http://DOMAIN_NAME](http://DOMAIN_NAME)" | tee -a /etc/hosts