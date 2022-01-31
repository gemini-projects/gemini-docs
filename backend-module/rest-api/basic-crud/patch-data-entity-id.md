---
description: PARTIAL MODE entity record update
---

# PATCH /data/{entity}/{id}

This API can be used for updating a record with the _**PARTIAL**_ mode. Partial means that only the fields in the data request body will be updated.

This API can be very useful when you have entities with a lot of fields and you want only to touch only some of them.

## Request

### Endpoint

```
PATCH <base_url>/data/{entity}/{id}
```

_**{entity}**_ is the Entity name according to the name provided in the schema

_**{id}**_ is the record identifier (the logical key for the record)&#x20;

### [Body - same as POST](post-data-entity.md#body)

## [Responses - same as POST](post-data-entity.md#responses)&#x20;
