---
description: GET all the data coming from an entity
---

# GET All Data

This API can be used to retrieve all the records belonging to a Single Entity. All the records means that the data driver scan all the Entity records to produce the resulting response JSON. This may be useful of course for small entities and in general for all the entities that don't need to be paginated. &#x20;

{% hint style="danger" %}
If this API may work well for entities up to some thousands of records, it is discouraged to GET all the records of an Entity that contains millions or billions records. For this kind of entities use [Pagination](pagination.md).

For big entities it is suggested to disable this API, in order to avoid queries that stuck the database or your system. You can disable the GET All Data API by using the [Rest Entity Configuration](../rest-configuration/big-entities.md).
{% endhint %}

## Request

### Endpoint

```
GET <base_url>/data/{entity}
```

_**{entity}**_ is the Entity name according to the name provided in the schema

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

Success response contains the list of all the data records.

```shell
curl "http://localhost:8080/data/category/"
```

```json
{
    "status": "success",
    "data": [{
        "description": "Smartphone",
        "id": "smartphone-1"
    },{
        "description":"Clothing",
        "id":"clothing-1"
    }]
}
```
