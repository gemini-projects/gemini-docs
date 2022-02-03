---
description: To GET entity data in a paginated way
---

# Pagination

This API is extremely useful when you have entities with a lot of records and you want to retrive data in batch, maybe with [filters](filters.md) or [sorters](sorting.md).

## Request

### Endpoint

```
GET <base_url>/data/{entity}?start={start}&limit={limit}
```

_**{entity}**_ is the Entity name according to the name provided in the schema

_**{limit}**_ is the max records returned from the api

_**{start}**_ you can control when to start to read

With a combination of _**start**_ and _**limit**_ you can navigate the entity with a pagination strategy where the limit parameter is the page size and the start is used to skip already read records.
