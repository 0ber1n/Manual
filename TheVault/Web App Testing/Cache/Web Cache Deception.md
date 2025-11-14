Need to find how a server is storing the cache. Add additional endpoints to see if it returns the same page such as /my-account/foo.js  

If it does, then send back to back to see if the cache hits. 


Payload hosted on attacker server to get page contents from deceptive web cache:
```js
<script>document.location="https://YOUR-LAB-ID.web-security-academy.net/PATH/SOMEFILE.js"</script>
```

You would then deliver this to victim and then try to pull the cached page on Burp.


### Delimiter Discrepancies

Must find a character that the server sees as a delimiter and not part of the path. Try different characters like /path;script  or /path,script  to see if you get the base response. Once found, set the path to a static page like done in normal deception and send the payload:
```js
<script>document.location="https://YOUR-LAB-ID.web-security-academy.net/PATH;SOMEFILE.js"</script>
```


