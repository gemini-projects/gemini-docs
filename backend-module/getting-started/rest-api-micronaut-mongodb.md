# REST API - Micronaut MongoDB

This is a _**Micronaut**_ starter project that use the basic features of Gemini and store data by using the MongoDb driver. To start you just need _**Docker**_ and a _**MongoDB**_ database (you can use the free [MongoDB Atlas](https://www.mongodb.com/atlas/database) cloud database)

In the [repository page](https://github.com/gemini-projects/gemini-micronaut/tree/main/starters/gemini-micronaut-mongodb-restapi) there is a full tutorial where in a matter of minutes you can see:

* how to define a simple Gemini Schema to describe your data
* how to run a Gemini REST API service using Docker and MongoDB
* how to start interacting with basic CRUD REST API over your data model
* how to use advanced APIs like counts, search and filters
* how to order data results and use pagination
* how to configure REST APIs

Let's see some of the main tutorial concepts here....

### Step 1 - Define the Schema

Schema is your data model, it is a YAML file that Gemini uses to generate all the API controllers and to map data.

```yaml
type: ENTITY
entity:
  name: CATEGORY
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
    - name: status
      type: ENUM
      enums: [DRAFT, PENDING, PRIVATE, PUBLISH]
    - name: regular_price
      type: DOUBLE
    - name: sale_price
      type: DOUBLE
    - name: categories
      type: ARRAY
      array:
        type: ENTITY_REF
        entityRef:
          entity: CATEGORY
```

### Step 2 - Run the Docker Image

After defining the data schema, we can start Gemini, exposing all the REST APIs. You can see further documentation for the env variables in the [repo tutorial](https://github.com/gemini-projects/gemini-micronaut/tree/main/starters/gemini-micronaut-mongodb-restapi#step-2---run-the-docker-image).

```
docker run -p 8080:8080 \
-e GEMINI_SCHEMAS=/schemas/product_schema.yaml \
-e GEMINI_MONGODB_URL="mongodb+srv://_mongo_user:_mongo_pwd_@__path__.mongodb.net/db?retryWrites=true&w=majority" \
-e GEMINI_MONGODB_DB=starter \
-v $(pwd)/product_schema.yaml:/schemas/product_schema.yaml:ro \
aat7/gemini-micronaut-mongodb-restapi
```

{% hint style="info" %}
This is the easiest way to start Gemini. Please note that in the previous Docker command we simply specify a Gemini Schema, and the Data Driver (MongoDB) parameters.

Below (and better in the [repo tutorial](https://github.com/gemini-projects/gemini-micronaut/tree/main/starters/gemini-micronaut-mongodb-restapi#big-entities)) it is also possibile to provide a REST API configuration, for example to handle big data entities.
{% endhint %}

### Step 3 - Use the REST APIs

Common APIS are CRUD REST APIs to insert, modify, delete and get data.

The url pattern for a particular entity is  `<base_url>/data/{entityName}`

Here is a list of some curl CRUD calls, but take a look at the [repo tutorial](https://github.com/gemini-projects/gemini-micronaut/tree/main/starters/gemini-micronaut-mongodb-restapi#step-3---use-some-basic-rest-apis) to see also responses and further details.

```shell
# POST data to add a category
curl --request POST "http://localhost:8080/data/category" \
--header "Content-Type: application/json" \
-d '{"data": {"id": "tech-1",
        "description": "Technology"
    }
  }'
  
# GET ALL data for an entity
curl "http://localhost:8080/data/category"

# GET ID 
curl "http://localhost:8080/data/category/smartphone-1"

```

### Step 4 - Count and Filter APIs

Gemini supports also other APIs like the count, and special filters (based on field types). Take a look at the [repo tutorial](https://github.com/gemini-projects/gemini-micronaut/tree/main/starters/gemini-micronaut-mongodb-restapi#step-3---use-some-basic-rest-apis) to see also responses and further details.

To count record simply use a GET with the url pattern `/entity/{entityName}/recordCounts`.&#x20;

```
curl "http://localhost:8080/entity/product/recordCounts"
```

Filters instead can be specified with common query string parameters. They works both with _data_ APIs and _recordCounts_ API.

Some examples to filter out and count specific products (remember to a look at the [repo tutorial](https://github.com/gemini-projects/gemini-micronaut/tree/main/starters/gemini-micronaut-mongodb-restapi#step-3---use-some-basic-rest-apis) to have more details and explanations):

```
# Count - Iphone 13 128 GB Blue - NB: the space is %20 in curl url
curl "http://localhost:8080/entity/product/recordCounts?name=Iphone%2013%20128%20GB%20Blue"
{"status":"success","data":{"count":1},"meta":{"elapsedTime":"38ms"}}

# Get Record - Iphone 13 128 GB Blue
curl "http://localhost:8080/data/product?name=Iphone%2013%20128%20GB%20Blue"
{"status":"success","data":[{"regular_price":799.0,"name":"Iphone 13 128 GB Blue","available":true,"description":"Apple Iphone 13 - Memory: 128 GB - Color: Blue","id":"iphone-13-128-blue","categories":["tech-1","smartphone-1"],"sale_price":699.0,"status":"PUBLISH"}],"meta":{"elapsedTime":"49ms"}}

# Count products with price GT (Greather Than >) 700
curl "http://localhost:8080/entity/product/recordCounts?regular_price[GT]=700"
{"status":"success","data":{"count":10},"meta":{"elapsedTime":"40ms"}}

# 10 products with price >= 799 
curl "http://localhost:8080/entity/product/recordCounts?regular_price[GTE]=799"
{"status":"success","data":{"count":10},"meta":{"elapsedTime":"39ms"}}

```

### Step 5 - Pagination & Big Entities

Gemini provide pagination out of the box for all the entities. Just use the _**start**_ and the _**limit**_ query string parameters to provide page size a navigate among pages and records. You can decide the pagesize by yourself with _**limit**_ and go to the next page with _**start**_.

```
# First page of 2 elements for the category Entity
curl "http://localhost:8080/data/category/?start=0&limit=2"

# Continue with the page number 2
curl "http://localhost:8080/data/category/?start=2&limit=2"
```

Usually you don't want to allow the GET ALL data API for very big entities (with thousands or millions records). In this situation you want the pagination to work as default behaviour.

You can achieve this goal providing a _**REST configuration**_ and specifying the default _**limit**_. In the repository documentation you can find an example YAML file (_restconfig.yaml_) available for you.

```
# restconfig.yaml 

type: ENTITY
entity: PRODUCT
config:
  getListStrategy: START_LIMIT
  defaultLimit: 5
```

Now let's use the new file _restconfig.yaml_ to provide the rest configuration for the _Product_ entity. Always take a look [here](https://github.com/gemini-projects/gemini-micronaut/tree/main/starters/gemini-micronaut-mongodb-restapi#big-entities) to know more about docker parameters.

```
docker run -p 8080:8080 \
        -e GEMINI_SCHEMAS=/schemas/product_schema.yaml \
        -e GEMINI_REST_CONFIGS=/rest/restconfig.yaml \
        -e GEMINI_MONGODB_URL="mongodb+srv://root:KK4b5sKopoyGDIy3@cluster0.9thyu.mongodb.net/db?retryWrites\=true&w\=majority" \
        -e GEMINI_MONGODB_DB=testdb_1 \
        -v $(pwd)/product_schema.yaml:/schemas/product_schema.yaml:ro \
        -v $(pwd)/restconfig.yaml:/rest/restconfig.yaml:ro \
        aat7/gemini-micronaut-mongodb-restapi

```

The service is running so let's make a simple call to count the _products_. As you can see from the curl command, the count API returns 560 records.

```
curl "http://localhost:8080/entity/product/recordCounts"
{"status":"success","data":{"count":560},"meta":{"elapsedTime":"57ms"}}
```

Now let's make a GET call to the the Products root. We don't add the _**limit**_ parameter but the framework automatically assign to the API the _**limit=5**_. Just take a look at the result, and the _**limit**_ field inside the _**meta**_ response body object (at the end of the JSON response).

```
curl "http://localhost:8080/data/product/"
{"status":"success","data":[{"regular_price":799.0,"name":"Iphone 13 128 GB Blue","available":true,"description":"Apple Iphone 13 - Memory: 128 GB - Color: Blue","id":"iphone-13-128-blue","categories":["tech-1","smartphone-1"],"sale_price":699.0,"status":"PUBLISH"},{"regular_price":799.0,"name":"Iphone 13 128 GB Starlight","available":true,"description":"Apple Iphone 13 - Memory: 128 GB - Color: Starlight","id":"iphone-13-128-starlight","categories":["tech-1","smartphone-1"],"sale_price":699.0,"status":"PUBLISH"},{"regular_price":799.0,"name":"Iphone 13 128 GB Midnight","available":true,"description":"Apple Iphone 13 - Memory: 128 GB - Color: Midnight","id":"iphone-13-128-midnight","categories":["tech-1","smartphone-1"],"sale_price":699.0,"status":"PUBLISH"},{"regular_price":799.0,"name":"Iphone 13 128 GB Pink","available":true,"description":"Apple Iphone 13 - Memory: 128 GB - Color: Pink","id":"iphone-13-128-pink","categories":["tech-1","smartphone-1"],"sale_price":699.0,"status":"PUBLISH"},{"regular_price":799.0,"name":"Iphone 13 128 GB Red","available":true,"description":"Apple Iphone 13 - Memory: 128 GB - Color: Product RED","id":"iphone-13-128-red","categories":["tech-1","smartphone-1"],"sale_price":699.0,"status":"PUBLISH"}],"meta":{"limit":5,"start":0,"elapsedTime":"43ms"}}
```

### Next Steps

Now that you are able to use all the basic features of Gemini you can start to model your own use case, so your own entities and data schema. If the mongo driver is enough for you just use the docker starter, otherwise you could develop your own [data driver](../data-drivers.md).
