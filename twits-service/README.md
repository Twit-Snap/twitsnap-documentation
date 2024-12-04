# Open API specification

```yaml
---
openapi: 3.1.0
info:
    title: Twits service
    description: Service to manage twitsnapp twits
    version: 1.0.0
paths:
    "/snaps/":
        post:
            description: ""
            responses:
                default:
                    description: ""
        get:
            description: ""
            parameters:
                - name: createdAt
                  in: query
                  type: string
                - name: limit
                  in: query
                  type: string
                - name: offset
                  in: query
                  type: string
                - name: older
                  in: query
                  type: string
                - name: has
                  in: query
                  type: string
                - name: username
                  in: query
                  type: string
                - name: byFollowed
                  in: query
                  type: string
                - name: hashtag
                  in: query
                  type: string
                - name: rank
                  in: query
                  type: string
                - name: exactDate
                  in: query
                  type: string
                - name: withEntities
                  in: query
                  type: string
                - name: noJoinParent
                  in: query
                  type: string
                - name: parent
                  in: query
                  type: string
                - name: type
                  in: query
                  type: string
                - name: bookmarks
                  in: query
                  type: string
            responses:
                "200":
                    description: OK
    "/snaps/amount":
        get:
            description: ""
            parameters:
                - name: createdAt
                  in: query
                  type: string
                - name: has
                  in: query
                  type: string
                - name: username
                  in: query
                  type: string
                - name: hashtag
                  in: query
                  type: string
                - name: exactDate
                  in: query
                  type: string
            responses:
                "200":
                    description: OK
    "/snaps/trending":
        get:
            description: ""
            responses:
                "200":
                    description: OK
    "/snaps/{id}":
        get:
            description: ""
            parameters:
                - name: id
                  in: path
                  required: true
                  type: string
            responses:
                default:
                    description: ""
        delete:
            description: ""
            parameters:
                - name: id
                  in: path
                  required: true
                  type: string
            responses:
                default:
                    description: ""
        patch:
            description: ""
            parameters:
                - name: id
                  in: path
                  required: true
                  type: string
            responses:
                default:
                    description: ""
    "/likes/twits/{twitId}":
        get:
            description: ""
            parameters:
                - name: twitId
                  in: path
                  required: true
                  type: string
            responses:
                default:
                    description: ""
    "/likes/":
        post:
            description: ""
            responses:
                default:
                    description: ""
        delete:
            description: ""
            responses:
                default:
                    description: ""
    "/likes/user/":
        get:
            description: ""
            responses:
                "200":
                    description: OK
    "/bookmarks/twits/{twitId}":
        get:
            description: ""
            parameters:
                - name: twitId
                  in: path
                  required: true
                  type: string
            responses:
                default:
                    description: ""
    "/bookmarks/":
        post:
            description: ""
            responses:
                default:
                    description: ""
        delete:
            description: ""
            responses:
                default:
                    description: ""
    "/twitShare/{twitId}":
        get:
            description: ""
            parameters:
                - name: twitId
                  in: path
                  required: true
                  type: string
            responses:
                "500":
                    description: Internal Server Error
```
