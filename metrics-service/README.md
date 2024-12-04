# Installation and Configuration

## Development 

### Clone the Repository:
```
git clone https://github.com/Twit-Snap/metrics_service.git
cd metrics_service
```
### Install Dependencies:
```
npm install
```
#### Set Up Environment Variables:
Create a .env file in the root directory and add the following:

```
DATABASE_URL=postgresql://myuser:mypassword@localhost:5431/twitter_metrics
NODE_ENV=development
API_LOCATION_KEY=99668cd0d2b64057b83e43a90ad34630
API_LOCATION_URL=https://api.opencagedata.com/geocode/v1/json
```

### Start Server:

The next command initialize the database in docker and start the server with nodemon.
```
npm run dev
```
### Testing and 
```
npm run test
```

### Architecture Definition

The service is built using the following technologies:
- TypeScript: As principal language.  
- Express: As handler of HTTP requests.
- PostgreSQL: As the database.
- Docker: For containerization of the database.
- Nodemon: For automatic server restarts during development.


# Layer Structure

The service is divided into the following layers:

- **Routes**: Contains the route definitions for the service.
- **Controllers**: Contains the logic for handling requests and validation of parameters send to the service.
- **Services**: Contains the business logic of the service and interacts with the database depending on the request.
- **Database**: Contains the database connection and handle the queries to interact with them.
- **Middlewares**: Contains the middlewares used in the service. Containing a log middleware and an error handler middleware. The log middleware logs the request and response of the service, while the error handler middleware catches any error that occurs during the request and sends a response with the error message.
- **Types**: Defines TypeScript types and interfaces.
- **Utils**: Contains utility functions and helpers.


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
