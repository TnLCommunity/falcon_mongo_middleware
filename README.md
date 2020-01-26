# mongo_middleware

A falcon middleware for mongo with some built in db naming/index structure logic.  It allows for schema generation and payload validation

Pypy compatible.

### Installation

`pip install falcon_mongo_middleware`

Or use poetry.

### Notes

Uses `MONGODB_URI` environment variable for what mongo to connect to.  

The Schemas module named by the `MONGODB_SCHEMA_PATH` will validate any kinds of objects you wish, as well as create indexes if they do not exist.  JSON Schema style dictionaries like the following example are the format:

```
my_field = {
    "type": "object",
    "properties": {
        "name": {"type": "string", "minLength": 1, "maxLength": 1000},
        "someVariable": {"type": "string", "minLength": 1, "maxLength": 1000}
    },
    "additionalProperties": False,
    "required": ["name", "someVariable"]
}
```

In your application, add the middleware to your falcon API:

```
from falcon_mongo_middleware.mongo_middleware import MongoMiddleware

mongo_middleware = MongoMiddleware()
api = application = falcon.API(middleware=[mongo_middleware])
```