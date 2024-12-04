# Requirements

-   Python 3.11
-   Docker 27.3.1
-   Makefile (Optional)
-   Firebase project serviceAccountKey.json

# Install

First, clone the repository

```bash
git clone https://github.com/Twit-Snap/message-service.git
```

or

```bash
git clone git@github.com:Twit-Snap/message-service.git
```

Then, copy inside src/ folder the serviceAccountKey.json from your firebase project.

# Run it

### Build

```bash
docker build -t image-message-service . # build it
```

or

```bash
make build
```

### Run

```bash
docker run --name message-service -p 8082:8082 image-message-service # run it
```

or

```bash
make run
```

### Stop & Clean container

```bash
docker stop message-service && docker rm message-service # stop & clean container
```

or

```bash
make stop
```

### Clean image

```bash
docker rmi image-message-service # clean image
```

or

```bash
make clean
```

### Run tests

```bash
pytest -v # run tests
```

or

```bash
make test
```

# Secrets and environment variables

USERS_SERVICE_URL: Url to twitsnap users service
JWT_SECRET_KEY: JWT generator key

### Firebase

You must need to configure the secret DATABASE_URL to an url of a real-time database from firebase and serviceAccountKey.json file content in base64 to SECRET_ACCOUNT_KEY.

### New Relic

If you want to use New Relic to monitor the service, you must need to configure the secrets NEW_RELIC_APP_NAME and NEW_RELIC_LICENSE_KEY

# Architecture

This service has the following architecture:

-   Controller layer: Validates data received from HTTP requests
-   Service layer: Bussiness logic and sending data to the repository
-   Repository layer: Connects to the firebase real-time database

# Open API specification

```yaml
---
openapi: 3.1.0
info:
    title: Message service
    description: Service to validate and send Twitsnapp direct messages
    version: 0.1.0
paths:
    "/chats":
        post:
            tags:
                - chats
            summary: Create a chat and get its id
            operationId: create_chat_chats_post
            requestBody:
                content:
                    application/json:
                        schema:
                            "$ref": "#/components/schemas/ChatBase"
                required: true
            responses:
                "201":
                    description: Successful Response
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/Chat"
                "422":
                    description: Validation Error
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/HTTPValidationError"
    "/chats/{id}":
        post:
            tags:
                - chats
            summary: Post a message in the chat {id}
            operationId: send_message_chats__id__post
            parameters:
                - name: id
                  in: path
                  required: true
                  schema:
                      type: string
                      title: Id
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            "$ref": "#/components/schemas/MessageBase"
            responses:
                "201":
                    description: Successful Response
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/Message"
                "422":
                    description: Validation Error
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/HTTPValidationError"
    "/chats/{chat_id}/messages/{id}":
        patch:
            tags:
                - chats
            summary: Edit content of chat message
            operationId: edit_message_chats__chat_id__messages__id__patch
            parameters:
                - name: id
                  in: path
                  required: true
                  schema:
                      type: string
                      title: Id
                - name: chat_id
                  in: path
                  required: true
                  schema:
                      type: string
                      title: Chat Id
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            "$ref": "#/components/schemas/MessageBase"
            responses:
                "200":
                    description: Successful Response
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/Message"
                "422":
                    description: Validation Error
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/HTTPValidationError"
        delete:
            tags:
                - chats
            summary: Delete a message
            operationId: delete_message_chats__chat_id__messages__id__delete
            parameters:
                - name: id
                  in: path
                  required: true
                  schema:
                      type: string
                      title: Id
                - name: chat_id
                  in: path
                  required: true
                  schema:
                      type: string
                      title: Chat Id
            responses:
                "204":
                    description: Successful Response
                "422":
                    description: Validation Error
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/HTTPValidationError"
components:
    schemas:
        Chat:
            properties:
                user1:
                    "$ref": "#/components/schemas/User"
                user2:
                    "$ref": "#/components/schemas/User"
                id:
                    type: string
                    title: Id
            type: object
            required:
                - user1
                - user2
                - id
            title: Chat
        ChatBase:
            properties:
                user1:
                    "$ref": "#/components/schemas/User"
                user2:
                    "$ref": "#/components/schemas/User"
            type: object
            required:
                - user1
                - user2
            title: ChatBase
        HTTPValidationError:
            properties:
                detail:
                    items:
                        "$ref": "#/components/schemas/ValidationError"
                    type: array
                    title: Detail
            type: object
            title: HTTPValidationError
        Message:
            properties:
                content:
                    type: string
                    title: Content
                id:
                    type: string
                    title: Id
                sender_id:
                    type: integer
                    title: Sender Id
                created_at:
                    type: string
                    title: Created At
            type: object
            required:
                - content
                - id
                - sender_id
                - created_at
            title: Message
        MessageBase:
            properties:
                content:
                    type: string
                    title: Content
                receiver_expo_token:
                    anyOf:
                        - type: string
                        - type: "null"
                    title: Receiver Expo Token
            type: object
            required:
                - content
            title: MessageBase
        User:
            properties:
                id:
                    type: integer
                    title: Id
                username:
                    type: string
                    title: Username
            type: object
            required:
                - id
                - username
            title: User
        ValidationError:
            properties:
                loc:
                    items:
                        anyOf:
                            - type: string
                            - type: integer
                    type: array
                    title: Location
                msg:
                    type: string
                    title: Message
                type:
                    type: string
                    title: Error Type
            type: object
            required:
                - loc
                - msg
                - type
            title: ValidationError
```
