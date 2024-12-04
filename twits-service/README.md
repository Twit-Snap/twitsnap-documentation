# Requirements

-   NodeJS 20
-   Docker 27.3.1
-   Docker-compose 2.6.0

# Install

First, clone the repository

```bash
git clone https://github.com/Twit-Snap/twits_service.git
```

or

```bash
git clone git@github.com:Twit-Snap/twits_service.git
```

Then, if you want to install the requirements to continue with the development run:

```bash
npm i
```

# Run it

### Run in development

```bash
npm run dev
```

### Run in production

#### Build

```bash
npm run build
```

#### Run

```bash
npm run start
```

### Run linter

```bash
npm run lint
```

### Run tests

#### Run

```bash
npm run test
```

#### Coverage

```bash
npm run coverage
```

# Secrets and environment variables

MONGODB_URI: Uri to mongo database, default = mongodb://localhost:27017/snapmsg. If you want to modify it, you can do so in docker-compose.yaml

FEED_ALGORITHM_URL: Url to twitsnap feed algorithm service

USERS_SERVICE_URL: Url to twitsnap users service

METRICS_SERVICE_URL: Url to twitsnap metrics service (optional)

JWT_SECRET_KEY: JWT generator key

### New Relic

If you want to use New Relic to monitor the service, you must need to configure the secrets NEW_RELIC_APP_NAME and NEW_RELIC_LICENSE_KEY

# Architecture

This service has the following architecture:

-   Controller layer: Validates data received from HTTP requests
-   Service layer: Bussiness logic and communicates with the repository
-   Repository layer: Makes queries to the mongo database

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
