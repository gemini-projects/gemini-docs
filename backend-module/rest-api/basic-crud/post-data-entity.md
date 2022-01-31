---
description: To add data and records to a generic Entity
---

# POST /data/{entity}

This API can be used to add records in a generic Gemini Entity. The API support both a single record and also a list of record to insert. This could be useful for example if the data driver you choose supports transactions, and you want to insert records in a single one.

## Request

### Endpoint

```
POST <base_url>/data/{entity}/
```

_**{entity}**_ is the Entity name according to the name provided in the schema

### Body

The request body is always a JSON containing the record actual data inside the _**data**_ field. The nested object inside the data field should follow the entity definition and the fields data types. Take a look at the [fields documentation](../../the-schema-ddd/fields/) to see examples and specific field syntax.

#### Add a Single Record&#x20;

```json
{
  "data": {
      // data fields according to the schema definition
  }
}
```

#### Add a List of Records

```json
{
  "data": [
     { 
        // record 1 - data fields according to the schema definition
     },
     {
        // record 2 - data fields according to the schema definition
     }
  ]
}
```

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

Success response contains the data inserted (record or list or records) and some useful metadata, for example the last update time in both ISO and unix format.

```shell
curl --request POST "http://localhost:8080/data/category" \
--header "Content-Type: application/json" \
-d '{"data": {"id": "tech-1",
        "description": "Technology"
    }
  }'
```

```json
{
  "status": "success",
  "data": {
    "description":"Technology",
    "id":"tech-1"
  },
  "meta": {
    "lastUpdateTimeUnix":1640185713731, 
    "lastUpdateTimeISO":"2021-12-22T15:08:33.731Z", 
  }
}
```

### 400 - Bad Request

Bad request errors means that the record cannot be inserted due to some errors in the entity record validation: for example an already existent logical key or a validation error, or an error during the data fields conversion.

```json
{
    "status": "error",
    "error": {
        "reason": "Logical key tech-1 for Entity CATEGORY already exists"
    }
}
```
