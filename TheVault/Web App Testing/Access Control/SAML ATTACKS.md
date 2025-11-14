
## Signature Stripping

#### Remove Signature
Remove the items of the signature tag but not the tag and send the response:
```
<ds:SignatureVAlue>
```

## Signature Wrapping

#### Missing Assertion (Error Grab)

1. Grab the SAML Request, send to repeater and create an error (can delete part of it)
2. Copy the response of the error-ed out response and paste it whole in to a text  file or through terminal file.
![](samlwrap_assertion.png)
3. Forward the request.
4. Take the entire SAML request decoded (from SAML raider) and add it to the text file immediately after the response captured. *Add a new line*.
5. Edit the open and close tags of the second response to delete the 'samlp:' part. 
6. Edit the the nameID to something else like the admins.
7. Delete the entire 'ds:SignatureValue' including tags from the second response portion.
8. That the newly created SAML response with the two root entities. Encode it into b64 then URL. 
9. Replace that URL in the SAML Response and send it.
10. Should be logged in as that new user.

## SAML Command Injection

#### Comment Injection
1. register an account on the IDP similar to the one you want to be but add more to the end of it that can been commented out like adminFAKE.
2. Capture the SAML response in SAML Raider, and add a comment between the nameID and the added gibberish such as the following:
```XML
admin<!--COMMENT-->FAKE
```
3. Send it. This should have the parser ignore the nameID at the comment and after.

