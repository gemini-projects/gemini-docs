---
description: GET entity record by id (logical key)
---

# GET /data/{entity}/{id}

When you need a specific entity record and you know the id (logical key).

## Request

### Endpoint

```
GET <base_url>/data/{entity}/{id}
```

_**{entity}**_ is the Entity name according to the name provided in the schema

_**{id}**_ is the record identifier (the logical key for the record)&#x20;

## Responses

Gemini responses always contains a proper HTTP status code, and a JSON body with a _status_ text, the _data_ inserted and a _meta_ object that holds metadata about the response_._

Lets take a look by using some real examples and the following schema:

```yaml
type: ENTITY
entity:
  name: CATEGORY
  lk: [id]
  fields:
    - name: id
      type: STRING
      required: true
    - name: description
      type: STRING
```

### 200 - Success

Success response contains the data record and some useful metadata, for example the last update time in both ISO and unix format.

```shell
curl "http://localhost:8080/data/category/smartphone-1"
```

```json
{
    "status": "success",
    "data": {
        "description": "Smartphone",
        "id": "smartphone-1"
    },
    "meta": {
        "lastUpdateTimeUnix": 1640185956675,
        "lastUpdateTimeISO": "2021-12-22T15:12:36.675Z",
    }
}
```

### 404 - Not Found

```
curl "http://localhost:8080/data/category/smartphone-noex"
```

```json
{
    "status": "error",
    "error": {
        "reason": "EntityRecord with id smartphone-noex not found for CATEGORY"
    }
}
```
