# Number

In Gemini a number can be of the following types: _**INTEGER**_, _**DOUBLE**_, _**DECIMAL**_&#x20;

```yaml
type: ENTITY
entity:
  name: PRODUCT
  displayName: Product
  lk: [id]
  fields:
    - name: id
      type: STRING
      required: true
    - name: weight
      type: DOUBLE
    - name: price
      type: DECIMAL
    - name: quantity
      type: INTEGER
```

As the name suggests, _**integer**_ and _**double**_ are respectively numbers without and with floating point unit. _**Decimal**_ instead should be used we you need to represent a number with perfect accuracy, for example to handle money and financial data. Basically they should be used when you don't want an approximation for your number, as the double data type does.&#x20;

The purpose of Gemini is to create REST APIs and its GUI. If your service need a more control on the data types you could re-map the Gemini types in what you want in the data driver.

{% hint style="warning" %}
Future releases will introduce validations and checking for numbers. For example _**min**_ or _**max**_ or inside some ranges.&#x20;
{% endhint %}
