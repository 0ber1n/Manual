## Upload Extension fuzzing

Whitelist extensions

[https:github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-extensions.txt](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/web-extensions.txt)

PHP Extensions
[https:github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Upload%20Insecure%20Files/Extension%20PHP/extensions.lst](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Upload%20Insecure%20Files/Extension%20PHP/extensions.lst)


Content-type, can download and filter specific known types; cat web-all-content-types.txt | grep 'image/' > image-content-types.txt

[https:raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Discovery/Web-Content/web-all-content-types.txt](https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Discovery/Web-Content/web-all-content-types.txt)

### CREDENTIAL CRACKING

Passwords

[https:raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/Common-Credentials/2023-200_most_used_passwords.txt](https://raw.githubusercontent.com/danielmiessler/SecLists/refs/heads/master/Passwords/Common-Credentials/2023-200_most_used_passwords.txt)

Usernames

[https:raw.githubusercontent.com/danielmiessler/SecLists/master/Usernames/top-usernames-shortlist.txt](https://raw.githubusercontent.com/danielmiessler/SecLists/master/Usernames/top-usernames-shortlist.txt)

```CLI
seclists/Usernames/xato-net-10-million-usernames.txt
```

Default Credentials

[https:www.cirt.net/passwords](https://www.cirt.net/passwords)

List of Cities

[https:github.com/datasets/world-cities/blob/main/data/world-cities.csv](https://github.com/datasets/world-cities/blob/main/data/world-cities.csv)

## DIRECTORIES

```CLI
/opt/useful/seclists/Discovery/Web-Content/directory-list-2.3-small.txt
```

LFI wordlists

[https:github.com/danielmiessler/SecLists/tree/master/Fuzzing/LFI](https://github.com/danielmiessler/SecLists/tree/master/Fuzzing/LFI)

[https:github.com/danielmiessler/SecLists/blob/master/Fuzzing/LFI/LFI-Jhaddix.txt](https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/LFI/LFI-Jhaddix.txt)

Server Webroot Linux

```CLI
/seclists/Discovery/Web-Content/default-web-root-directory-linux.txt
```

```CLI
/seclists/Discovery/Web-Content/default-web-root-directory-windows.txt
```

Server Logs/Configurations

[https:raw.githubusercontent.com/DragonJAR/Security-Wordlist/main/LFI-WordList-Linux](https://raw.githubusercontent.com/DragonJAR/Security-Wordlist/main/LFI-WordList-Linux)

[https:raw.githubusercontent.com/DragonJAR/Security-Wordlist/main/LFI-WordList-Windows](https://raw.githubusercontent.com/DragonJAR/Security-Wordlist/main/LFI-WordList-Windows)

**API**

```CLI
/usr/share/seclists/Discovery/Web-Content/common-api-endpoints-mazen160.txt
```

[https:wordlists.assetnote.io/](https://wordlists.assetnote.io/)