# Feed Algorithm Service

## Documentation starts here

Hello

# Open API specification

```yaml
---
openapi: 3.1.0
info:
    title: Tweet algorithm API
    description:
        This is a simple API for providing users with tweets similar to tweets
        they've interacted recently
    version: 1.0.0
paths:
    "/":
        post:
            summary: Refresh Index Content
            operationId: refresh_index_content__post
            requestBody:
                content:
                    application/json:
                        schema:
                            "$ref": "#/components/schemas/TweetRequest"
                required: true
            responses:
                "200":
                    description: Successful Response
                    content:
                        application/json:
                            schema: {}
                "422":
                    description: Validation Error
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/HTTPValidationError"
    "/rank":
        post:
            summary: Rank By Given Tweets
            operationId: rank_by_given_tweets_rank_post
            requestBody:
                content:
                    application/json:
                        schema:
                            "$ref": "#/components/schemas/TweetRequest"
                required: true
            responses:
                "201":
                    description: Successful Response
                    content:
                        application/json:
                            schema:
                                additionalProperties:
                                    "$ref": "#/components/schemas/TweetRanking"
                                type: object
                                title: Response Rank By Given Tweets Rank Post
                "422":
                    description: Validation Error
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/HTTPValidationError"
    "/trending":
        post:
            summary: Get Trending Topics
            operationId: get_trending_topics_trending_post
            requestBody:
                content:
                    application/json:
                        schema:
                            "$ref": "#/components/schemas/TrendingTopicRequest"
                required: true
            responses:
                "201":
                    description: Successful Response
                    content:
                        application/json:
                            schema:
                                additionalProperties:
                                    "$ref": "#/components/schemas/TrendingTopics"
                                type: object
                                title: Response Get Trending Topics Trending Post
                "422":
                    description: Validation Error
                    content:
                        application/json:
                            schema:
                                "$ref": "#/components/schemas/HTTPValidationError"
components:
    schemas:
        HTTPValidationError:
            properties:
                detail:
                    items:
                        "$ref": "#/components/schemas/ValidationError"
                    type: array
                    title: Detail
            type: object
            title: HTTPValidationError
        TrendingTopicRequest:
            properties:
                limit:
                    type: integer
                    title: Limit
            additionalProperties: false
            type: object
            required:
                - limit
            title: TrendingTopicRequest
        TrendingTopics:
            properties:
                data:
                    items:
                        additionalProperties:
                            type: integer
                        type: object
                    type: array
                    title: Data
            additionalProperties: false
            type: object
            required:
                - data
            title: TrendingTopics
        Tweet:
            properties:
                id:
                    type: string
                    title: Id
                content:
                    type: string
                    title: Content
            additionalProperties: false
            type: object
            required:
                - id
                - content
            title: Tweet
        TweetRanking:
            properties:
                data:
                    items:
                        "$ref": "#/components/schemas/Tweet"
                    type: array
                    title: Data
            additionalProperties: false
            type: object
            required:
                - data
            title: TweetRanking
        TweetRequest:
            properties:
                data:
                    items:
                        "$ref": "#/components/schemas/Tweet"
                    type: array
                    title: Data
                limit:
                    type: integer
                    title: Limit
            additionalProperties: false
            type: object
            required:
                - data
                - limit
            title: TweetRequest
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
