---
description: To get data already sorted by one or more field (ascending or descending)
---

# Sorting

Sorting can be use bot in [get-all-data.md](get-all-data.md "mention") or [pagination.md](pagination.md "mention") strategies. It is extremely useful for paginated APIs because for example you can start reading by name, or by date (ex: lastUpdate) and so on.

They can also be used in combination with [filters.md](filters.md "mention")

## Request

### Endpoint

```
GET <base_url>/data/{entity}?orderBy={field}
```

_**{entity}**_ is the Entity name according to the name provided in the schema

_**{field}**_ is the name of the field to order by. If you want to sort ASCENDING simply use the field name, but if you want to sort DESCENDING prefix the field name with a minus **-**

{% hint style="info" %}
**Remember:** you can use sorting with Filters and Pagination
{% endhint %}

### Examples

Lets take a look by using some examples and the following schema:

```yaml
type: ENTITY
entity:
  name: ORDER
  lk: [id]
  fields:
    - name: id
      type: STRING
      required: true
    - name: date
      type: DATE_TIME
    - name: status
      type: ENUM
      enum: [RECEIVED, SHIPPED]
    #
    # --- other fields
    #

```

#### DATE ASCENDING ORDER

And filtered by status SHIPPED, getting the first page with a page size of 20 records&#x20;

```shell
curl "<baseurl>/data/order?status=SHIPPED&orderBy=date&start=0&limit=20"
```

#### DATE DESCENDING ORDER (note the minus - before the field name)

And filtered by status RECEIVED, getting the first page with a page size of 20 records

```shell
curl "<baseurl>/data/order?status=RECEIVED&orderBy=-date&start=0&limit=20"
```
