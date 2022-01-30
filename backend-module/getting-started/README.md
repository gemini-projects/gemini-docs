# Getting Started

Getting started with the backend module is really simple. Use one the starters and follow the tutorial in the official repository to explore its features.

{% content-ref url="rest-api-micronaut-mongodb.md" %}
[rest-api-micronaut-mongodb.md](rest-api-micronaut-mongodb.md)
{% endcontent-ref %}

{% hint style="warning" %}
Gemini platform is under development. Full production ready features are reserved to companies that collaborates with the project or are interested to use the platform and need professional support.&#x20;

Professional and Enterprise use cases usually requires to implement custom drivers, or to combine gemini packages in order to create a full and stable production service.
{% endhint %}

### Source Code

_Gemini Micronaut (the backend module)_ is made of different packages that you can combine together accordingly to your needs. It is an open source project that you can find and explore [here](https://github.com/gemini-projects/gemini-micronaut).

For example you can use the out of the box data drivers or write your own code to store data where and how you want.

* _**core**_ is the main part of the framework, that implements the REST APIs common interface and loads the DDD schema
* _**auth**_ to add authentication to the APIs
* _**gcp-firebase**_ driver to store API data by using firebase
* _**mongodb**_ driver to store API data by using MongoDB
* _**adminspa**_ simple package that provide an easy schema to build a full Admin APP backend (menus, settings, users, and so on..)
