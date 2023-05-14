

## Calculator application

The calculator application uses a micro service architecture to provide an API to resolve mathematical expressions.

The calculator API exposes a single endpoint, a `POST` method on the `/` root url.
This endpoint receives an expression in the form of JSON:

Expression example:

```
curl -XPOST -H 'Authentication: Bearer binary-example' -H 'Content-Type: application/json' localhost:3000/ -d '{
    "type": "addition",
    "left": 6,
    "right": 1
}'
```

Expressions can be nested:

```
curl -XPOST -H 'Authentication: Bearer nested-example' -H 'Content-Type: application/json' localhost:3000/ -d '{
    "type": "addition",
    "left": {
       "type": "addition",
       "left": 6,
       "right": 1
    },
    "right": {
        "type": "subtraction",
        "left": {
            "type": "addition",
            "left": 6,
            "right": 1
        },
        "right": 1
    }
}'
```

The `calculator` micro service is the gateway where all calculator requests should be done.
The `calculator` service does not solve any expression by it self, it relies on a set of micro services to solve expressions.
There is one micro service per expression, all micro services only expose one endpoint, a `POST` method on the `/` root url and they expect an JSON expression with a numeric `left` and `right` operands.
The `calculator` service is responsible for navigating the expression nodes in such a way that it only calls the expression micro services only with number parameters.

The available mathematical expression micro services are:

-   `addition`:
    Returns a value object with the result of adding both operands.
-   `subtraction`:
    Returns a value object with the result of subtracting the `right` operand from the `left` one.
-   `multiplication`:
    Returns a value object with the result of multiplying both operands.
-   `division`:
    Returns a value object with the result of dividing the `left` by the `right` operand.
-   `remainder`:
    Returns a value object with the result of the remainder of dividing the `left` by the `right` operand.

**Note**:
"kilabs/cloud-engineer-challenge-calculator:latest" image is build from services/base/dockerfile

## Challenge 1. Debug skills

In the root of the project you have a docker-compose that brings all services up.
As you may notice the client service is not working properly and is throwing an error.
We need you to fix it!










