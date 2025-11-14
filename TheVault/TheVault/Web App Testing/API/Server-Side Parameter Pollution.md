#### Truncating query parameters

Truncating queries by adding URL encoded '#'.
```
GET /userSearch?name=peter%23foo&back/home
```
Where the API will try to access:
```
GET /userSearch?namepeter#foo&publicProfile=true
```
If the call returns an error, then it saw the '#foo' as part of the query but no error mean it was truncated.

#### Injecting Invalid Parameters

Add a URL encoded '&' to try and throw an additional query:
```
GET /userSearch?name=peter%26name=carlos&back/home
```
The API call being:
```
GET /userSearch?namepeter&fname=carlos&publicProfile=true
```

Different web techs see parameters different:
- PHP parses the last parameter only. This would result in a user search for `carlos`.
- ASP.NET combines both parameters. This would result in a user search for `peter,carlos`, which might result in an `Invalid username` error message.
- Node.js / express parses the first parameter only. This would result in a user search for `peter`, giving an unchanged result.

