# Metrics Service

## Requirements
- NodeJS 20
- Docker 27.3.1
- Docker-compose 2.6.0

# Installation 

First, clone the repository

``` bash 
git clone https://github.com/Twit-Snap/metrics_service.git
```
Then, if you want to install the requirements to continue with the development run:

``` bash 
npm install
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

- **DATABASE_URL:** Uri to Postgres database, default = postgresql://myuser:mypassword@localhost:5431/twitter_metrics. If you want to modify it, you can do so in docker-compose.yaml
- **NODE_ENV:** variable to set the environment of the service. It can be development or production. 
- **API_LOCATION_KEY:** API key to use the OpenCage API to get the location of a user based on the coordinates. You can obtain an API key from the OpenCage website.
- **API_LOCATION_URL:** https://api.opencagedata.com/geocode/v1/json


# Layer Structure

The service is divided into the following layers:

- **Routes**: Contains the route definitions for the service.
- **Controllers**: Contains the logic for handling requests and validation of parameters send to the service.
- **Services**: Contains the business logic of the service and interacts with the database depending on the request.
- **Database**: Contains the database connection and handle the queries to interact with them.
- **Middlewares**: Contains the middlewares used in the service. Containing a log middleware and an error handler middleware. The log middleware logs the request and response of the service, while the error handler middleware catches any error that occurs during the request and sends a response with the error message.


# Open API specification

```yaml
---
openapi: 3.1.0
info:
    title: Metrics service
    description: Service to manage twitsnapp metrics
    version: 1.0.0
paths:
    "/metrics/":
        post:
            description: ""
            responses:
                "201":
                    description: Created
        get:
            description: ""
            parameters:
                - name: type
                  in: query
                  type: string
                - name: username
                  in: query
                  type: string
                - name: dateRange
                  in: query
                  type: string
                - name: auth
                  in: query
                  type: string
            responses:
                "200":
                    description: OK
```
