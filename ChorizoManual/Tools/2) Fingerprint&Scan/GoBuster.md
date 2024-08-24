$sudo apt install golang-go 
$go install github.com/OJ/gobuster/v3@latest 

~running brute force directories 
$ gobuster dir --url http://10.10.10.10 -wordlist /usr/share/wordlists/SecLists/directory-list-2.3-small.txt 

~sub-domain enumeration 

$ gobuster vhost -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain -u [http://thetoppers.htb](http://thetoppers.htb)