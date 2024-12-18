# Feed Algorithm Service

## Requirements
- FastAPI 0.115.0
- Pytest 8.3.2
- python-dotenv 1.0.1
- Sentence Transformers 3.2.0
- nltk 3.9.1
- Faiss-CPU 1.9.0

# Installation

First, clone the repository

``` bash 
git clone https://github.com/Twit-Snap/feed_algo_service.git
```

## Running locally
1. Build the image
```
docker build -t dev-feed-algo .
```
2. Run the image (Memory and CPU limits are optional, but recommended to replicate the deployment environment)
```
docker run --name algo-feed -e HOST=0.0.0.0 -e PORT=8000 -p 8000:8000 --memory=600m --cpus=2 dev-feed-algo
```

## Running the test suite
1. Build the image
```
docker build -t dev-feed-algo .
```
2. Run the image with the env var MODE set on test
```
docker run --name algo-feed -e MODE=test dev-feed-algo
```

# Basic functionality

There are two main functionalities present in this service:
- Twit recommendation
- Trending topics generation

## Twit recommendation
A corpus of Twits is fed to the service, which encodes the content in them using a pre-trained model. The UUID's of the twits are saved separately from the vectorial database that holds the encoded twits.
Users then send a sample of twits they've recently interacted with which is then used to query similar twits from the database. The service returns the most similar twits to the ones provided by the user.
The Vectorial database is saved in memory using the [FAISS (Facebook AI Similarity Search) algorithm](https://github.com/facebookresearch/faiss).

## Trending topics generation
Given the same corpus of twits, the service generates a list of trending topics. The topics are generated by first tokenizing the twits and then counting the frequency of each token.
Twits are first tokenized, then filtered given a list of extended stopwords ([English stopwords by nltk](https://gist.github.com/sebleier/554280) + common words present in twits).
The service then counts the frequency of each token and returns the _n_ most frequent ones.

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
