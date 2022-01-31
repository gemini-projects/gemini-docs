# Overview

The Gemini Backend module is built on top of the _Java Micronaut Framework_ providing an easy way to create powerful _**REST APIs**_ using a _**Domain Driven Design**_ approach.

### How it works

#### The Schema

The starting point of Gemini is the _Gemini Schema_, by using a _Domain Driven Design_ approach developers can define the data fields for the APIs letting Gemini doing the REST.

{% content-ref url="the-schema-ddd/" %}
[the-schema-ddd](the-schema-ddd/)
{% endcontent-ref %}

#### The REST API

Starting from the schema, Gemini automatically generates for you:

* **Basic CRUD APIs:** GET, POST, PUT, PATCH, DELETE
* **Advanced APIS**: filter / count / search&#x20;
* **Big data support**: like pagination and sorting for entities with millions of records

Gemini also provide a way to define REST API configurations, letting the APIs behave as you want. For example you can decide to create read only entities so PUT, POST are disabled. Or you can enable pagination for big data entities in order to avoid an overload for the service.

{% content-ref url="rest-api/" %}
[rest-api](rest-api/)
{% endcontent-ref %}

#### The Data Drivers

The data driver is the low level of Gemini, where developer choose how to store or retrieve raw data. Usually in the drivers there is the mapping between fields of the _Gemini  Entities_ (defined in the schema) and the data storage of the driver (SQL, NoSql, files, queue, etc...).

{% content-ref url="data-drivers.md" %}
[data-drivers.md](data-drivers.md)
{% endcontent-ref %}

