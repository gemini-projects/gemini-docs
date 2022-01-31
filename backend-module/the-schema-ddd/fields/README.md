# Fields

Fields are the most important part of each entity. They describe the properties an entity holds and they can be of different types, from primitive ones (like strings, or integers) to complex like nested object, references or arrays.

### Field Configuration

Each field has the following properties, some required like the _name_ and the _type_ and some are optional like the _displayName_ and the _required_ field.

<table><thead><tr><th>Property</th><th>Description</th><th data-type="select">Required</th></tr></thead><tbody><tr><td>name</td><td>The name of the field. It is gonna to be used in all the Gemini framework, also with low level APIs in order to build the JSON properties and identify the field.</td><td></td></tr><tr><td>type</td><td>The data type for the field</td><td></td></tr><tr><td>required</td><td><em><strong>true</strong></em> or <em><strong>false</strong></em> to specify if the field is required when you insert or update the record or not. Default is <em>false.</em></td><td></td></tr><tr><td>displayName</td><td>If you want a different display name, especially for the GUI parts.</td><td></td></tr></tbody></table>

For example lets see a Product entity where the fields _id_, _name_ and _price_ are **required.**

```
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
      required: true
    - name: price
      type: DECIMAL
      required: true
    - name: salePrice
      displayName: Sale Price
      type: DECIMAL
```

{% hint style="info" %}
_displayName_ is useful for the frontend part. Using this field you can indicate a display name for the field label (for example in a form or in table) that is different from the label used inside JSON and APIs.&#x20;
{% endhint %}

### Field Types

Each field may contains its own configuration, especially complex fields like nested object, arrays, foreign keys and so on.

{% content-ref url="string.md" %}
[string.md](string.md)
{% endcontent-ref %}
