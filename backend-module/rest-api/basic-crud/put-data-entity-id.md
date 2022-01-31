---
description: FULL MODE entity record update
---

# PUT /data/{entity}/{id}

This API can be used for updating a record with _**FULL**_ mode. Full means that everything that the entity record is totally replaced with the data coming from the request body. So, for example if you want to erase a field, just not pass it in the body.

For updating only some fields you can use the [PATCH API](patch-data-entity-id.md).

## Request

### Endpoint

```
PUT <base_url>/data/{entity}/{id}
```

_**{entity}**_ is the Entity name according to the name provided in the schema

_**{id}**_ is the record identifier (the logical key for the record)&#x20;

### [Body - same as POST](post-data-entity.md#body)

## [Responses - same as POST](post-data-entity.md#responses)&#x20;
