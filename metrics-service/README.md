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
