# String

String is the primitive type to store any type of text. Usually a string field is used as a logical key for an entity record, like the example below for the entity with name _Category._

```yaml
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
```

{% hint style="warning" %}
Future releases will introduce validations and text/string checking that you can define both in a declarative way directly in the schema and both as a totally custom code.
{% endhint %}
