# Entities

The Gemini schema is very simple and self-explanatory. It is a simple YAML where you can put the list of your _**entities**_. The Gemini platform automatically reads entities and fields and provide for you all the API for inserting, updating and retrieving data with validation features.

### Common Entities

Here for example a very basic schema with two entities: _Product_ and _Category_ and some basic fields. Each entity always has a name and a list of fields.

Common entities are those one that can contains multiple records (like a table in SQL or a collection in NoSQL). For this reason each entity has also a logical key to identify a single record. The logical key (_lk_) can contain one or more fields, usually strings or sequence numbers.

```yaml
# EXAMPLE - PRODUCT AND CATEGORY SCHEMA DEFINITION

type: ENTITY
entity:
  name: CATEGORY
  displayName: Category
  lk: [id]
  fields:
    - name: id
      type: STRING
      required: true
    - name: description
      type: STRING

---

type: ENTITY
entity:
  name: PRODUCT
  displayName: Product
  lk: [id]
  fields:
    - name: id
      type: STRING
      required: true
    - name: name
      type: STRING
    - name: description
      type: STRING
    - name: available
      type: BOOL

```

### Entity Configuration

From the previous schema you can see some important configurations. Each Entity has:

<table><thead><tr><th>Property</th><th>Description</th><th data-type="select">Required</th></tr></thead><tbody><tr><td>name</td><td>The name of the Entity. It is gonna to be used in all the Gemini framework, also with low level APIs in order to retrieve the Entity Data or Configuration</td><td></td></tr><tr><td>lk</td><td>List of logical keys for the entity. Must be one or more fields of basic types. Usually numbers and strings. The fields order matters.</td><td></td></tr><tr><td>displayName</td><td>If you want a different display name, especially for the GUI parts, when you need to interact with entity configuration</td><td></td></tr><tr><td>fields</td><td>The list of fields for the Entity</td><td></td></tr></tbody></table>
