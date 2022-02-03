---
description: Filter Entity Data with query strings
---

# Filters

Filters are query string parameters that can be combined to select only data that match some criteria. You can use filters both with [get-all-data.md](get-all-data.md "mention") and [pagination.md](pagination.md "mention") strategies.

Of course you can provide multiple filters for different fields, and they are treated as AND filters.

Filters can be specialised according to its type, for example strings can be filtered with CONTAINS or START\_WITH, while numbers and dates can be filtered by range or arithmetic operations.

## Request

### Endpoint

#### Equals filter (works for all the types)

```
GET <base_url>/data/{entity}?{fieldName_1}={fieldValue_1}&{fieldName_2}={fieldValue_2}
```

#### Contains filter (works for strings)

```
GET <base_url>/data/{entity}?{fieldName_1}[CONTAINS]={fieldValue_1}
```

_**{entity}**_ is the Entity name according to the name provided in the schema_**{entity}**_ is the Entity name according to the name provided in the schema

_**{fieldName}**_ is the name of the field to filter

_**{fieldValue}**_ is the value to search

{% hint style="info" %}
**Remember:** you can use multiple filters (like _filter1 and filter_2).
{% endhint %}

{% hint style="warning" %}
Each field type as its own filters, for example CONTAINS for strings like the previous example. To see all the available operators take a look at the [Schema Fields](../../the-schema-ddd/fields/) documentation.
{% endhint %}

#### OR filters

Or filters are allowed when you specify multiple values for the same field. For example you could query a filter that is equals to a _value1_ or a _value2_.&#x20;

```
GET <base_url>/data/{entity}?{fieldName_1}={fieldValue_1}&{fieldName_1}={fieldValue_2}
```

{% hint style="warning" %}
OR filters can be used with all the operators, not only the classic equals =. For example to filter a number greater than X and less than Y at the same time. To see all the available operators take a look at the [Schema Fields](../../the-schema-ddd/fields/) documentation.
{% endhint %}
