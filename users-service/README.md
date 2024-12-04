# Open API specification

```yaml
---
openapi: 3.1.0
info:
    title: Users service
    description: Service to manage twitsnapp users
    version: 1.0.0
paths:
    "/auth/login":
        post:
            description: ""
            responses:
                default:
                    description: ""
    "/auth/register":
        post:
            description: ""
            responses:
                default:
                    description: ""
    "/auth/verify":
        post:
            description: ""
            responses:
                default:
                    description: ""
    "/auth/forgot-password":
        post:
            description: ""
            responses:
                default:
                    description: ""
    "/auth/reset-password":
        post:
            description: ""
            responses:
                default:
                    description: ""
    "/users/":
        get:
            description: ""
            parameters:
                - name: has
                  in: query
                  type: string
                - name: createdAt
                  in: query
                  type: string
                - name: limit
                  in: query
                  type: string
                - name: amount
                  in: query
                  type: string
                - name: offset
                  in: query
                  type: string
                - name: equalDate
                  in: query
                  type: string
            responses:
                "200":
                    description: OK
    "/users/interests":
        get:
            description: ""
            responses:
                "200":
                    description: OK
        post:
            description: ""
            parameters:
                - name: body
                  in: body
                  schema:
                      type: object
                      properties:
                          interests:
                              example: any
            responses:
                "200":
                    description: OK
    "/users/{username}":
        get:
            description: ""
            parameters:
                - name: username
                  in: path
                  required: true
                  type: string
                - name: reduce
                  in: query
                  type: string
                - name: suggestAccounts
                  in: query
                  type: string
                - name: limit
                  in: query
                  type: string
            responses:
                "200":
                    description: OK
        patch:
            description: ""
            parameters:
                - name: username
                  in: path
                  required: true
                  type: string
                - name: body
                  in: body
                  schema:
                      type: object
                      properties:
                          isBlocked:
                              example: any
            responses:
                "200":
                    description: OK
    "/users/{username}/followers":
        post:
            description: ""
            parameters:
                - name: username
                  in: path
                  required: true
                  type: string
                - name: body
                  in: body
                  schema:
                      type: object
                      properties:
                          followedUsername:
                              example: any
            responses:
                "201":
                    description: Created
        delete:
            description: ""
            parameters:
                - name: username
                  in: path
                  required: true
                  type: string
                - name: body
                  in: body
                  schema:
                      type: object
                      properties:
                          followedUsername:
                              example: any
            responses:
                "204":
                    description: No Content
    "/users/{username}/followers/":
        get:
            description: ""
            parameters:
                - name: username
                  in: path
                  required: true
                  type: string
                - name: byFollowers
                  in: query
                  type: string
                - name: has
                  in: query
                  type: string
                - name: createdAt
                  in: query
                  type: string
                - name: limit
                  in: query
                  type: string
            responses:
                "200":
                    description: OK
    "/users/{username}/followers/{followedUsername}":
        get:
            description: ""
            parameters:
                - name: username
                  in: path
                  required: true
                  type: string
                - name: followedUsername
                  in: path
                  required: true
                  type: string
            responses:
                "200":
                    description: OK
    "/users/location":
        post:
            description: ""
            parameters:
                - name: body
                  in: body
                  schema:
                      type: object
                      properties:
                          latitude:
                              example: any
                          longitude:
                              example: any
            responses:
                default:
                    description: ""
    "/users/notifications":
        post:
            description: ""
            parameters:
                - name: body
                  in: body
                  schema:
                      type: object
                      properties:
                          title:
                              example: any
                          body:
                              example: any
                          data:
                              example: any
            responses:
                default:
                    description: ""
    "/admins/users":
        get:
            description: ""
            parameters:
                - name: has
                  in: query
                  type: string
                - name: createdAt
                  in: query
                  type: string
                - name: offset
                  in: query
                  type: string
            responses:
                "200":
                    description: OK
    "/admins/users/{username}":
        get:
            description: ""
            parameters:
                - name: username
                  in: path
                  required: true
                  type: string
            responses:
                "200":
                    description: OK
    "/auth/admins/register":
        post:
            description: ""
            responses:
                "201":
                    description: Created
    "/auth/admins/login":
        post:
            description: ""
            responses:
                "200":
                    description: OK
    "/auth/sso/login":
        post:
            description: ""
            responses:
                default:
                    description: ""
    "/auth/sso/register":
        post:
            description: ""
            responses:
                default:
                    description: ""
    "/public/interests":
        get:
            description: ""
            responses:
                "200":
                    description: OK
    "/redirect/{path}":
        get:
            description: ""
            parameters:
                - name: path
                  in: path
                  required: true
                  type: string
            responses:
                default:
                    description: ""
```
