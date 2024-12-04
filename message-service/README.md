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
