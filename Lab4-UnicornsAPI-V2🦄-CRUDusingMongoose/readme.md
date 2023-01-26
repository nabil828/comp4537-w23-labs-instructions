To be submitted during lab hours

# Mongoose
Mongoose is an Object-Document Mapping (ODM) library for MongoDB and Node.js. It provides a straight-forward, schema-based solution to model your application data and includes built-in type casting, validation, query building, business logic hooks and more.

Mongoose allows you to define a schema for your collections in MongoDB, which is a blueprint for the documents within that collection. The schema defines the structure of the documents, including the fields and their types, and also allows you to specify validation rules and default values for the fields.

Once you have a schema, you can use it to create a Mongoose model, which provides an interface for interacting with the collection in MongoDB. You can use this model to create, read, update and delete (CRUD) documents in the collection.

Mongoose also provides middleware that allows you to run specific code before or after certain operations, such as saving a document or removing a document. This can be useful for handling tasks such as logging, auditing, and validation.

By using Mongoose, you can write MongoDB validation, casting and business logic in a more structured and organized way compared to MongoDB's native driver.

Here is an example of how you can use Mongoose to connect to a MongoDB database, create a schema, model, and perform CRUD operations in an Express.js server:

## Mongoose Connection
```js
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/test', { useNewUrlParser: true });

```


## Mongoose Schema 
```js
const unicornSchema = new mongoose.Schema({
  name: { type: String, required: true },
  dob: { type: Date, default: Date.now },
  loves: [String],
  weight: { type: Number, min: 0 },
  gender: { type: String, enum: ['m', 'f'] },
  vampires: { type: Number, min: 0 }
});
```


## Mongoose Model
```js
const Unicorn = mongoose.model('unicorns', unicornSchema);
```


# CRUD using Mongoose
CRUD operations in Mongoose can be performed by using the following methods:

1.  **Create**: Use the `Model.create(docs, [callback])` method to insert one or more documents into the collection.
```js
  Unicorn.create(req.body, (err, unicorn) => {
    if (err) return res.status(400).send(err);
    res.status(201).json(unicorn);
  });
```
OR
```js
  Unicorn.insertMany(req.body, (err, unicorns) => {
    if (err) return res.status(400).send(err);
    res.status(201).json(unicorns);
  });
```
OR
```js
  const newUnicorn = new Unicorn(req.body);
  newUnicorn.save((err, unicorn) => {
    if (err) return res.status(400).send(err);
    res.status(201).json(unicorn);
  });
```
Source - https://mongoosejs.com/docs/models.html#constructing-documents

2.  **Read**: Use the `Model.find(conditions, [projection], [options], [callback])` method to query the collection and retrieve documents that match the specified conditions.



```js
  Unicorn.findById(req.params.id, (err, unicorn) => {
    if (err) return res.status(400).send(err);
    if (!unicorn) return res.status(404).send();
    res.json(unicorn);
  });
```
Source - https://mongoosejs.com/docs/queries.html

3.  **Update**: Use the `Model.update(conditions, update, [options], [callback])` method to update one or more documents in the collection that match the specified conditions.  



```js
 Unicorn.findByIdAndUpdate(req.params.id, req.body, { new: true }, (err, unicorn) => {
    if (err) return res.status(400).send(err);
    if (!unicorn) return res.status(404).send();
    res.json(unicorn);
  });
```  
Source - https://mongoosejs.com/docs/api.html#model_Model-findByIdAndUpdate
<details>
<summary>
Question: which one do we usually use for mongodb update, HTTP PUT or HTTP PATCH? 
</summary>

When updating a resource in a MongoDB database using Mongoose and Express.js, the most commonly used HTTP verb is PATCH.

The reason for this is that PATCH is used to partially update a resource, which is often the case when updating a MongoDB document. This means that you can update only specific fields in a document without having to send the entire document to the server.

On the other hand, PUT is used to completely replace a resource. This means that you would need to send the entire document to the server, even if you only want to update a single field. This can be less efficient and less flexible.
</details>
<br>
<br>

4.  **Delete**: Use the `Model.remove(conditions, [callback])` method to remove one or more documents from the collection that match the specified conditions.



```js
 Unicorn.findByIdAndRemove(req.params.id, (err, unicorn) => {
    if (err) return res.status(400).send(err);
    if (!unicorn) return res.status(404).send();
    res.json(unicorn);
  });
```

Please note that, you need to first create a mongoose schema and Model to perform these operations.

# Lab 4 - Unicorns API - V2 🦄
## API Specifications 
Here is an example of a RESTful API specification for a simple "Unicorn🦄" application:

*   Endpoint: `/unicorns`
    *   `GET`: Retrieve a list of all unicorns
    *   `POST`: Create a new unicorn
*   Endpoint: `/unicorns/{id}`
    *   `GET`: Retrieve a specific unicorn by ID
    *   `PUT`: Update a specific unicorn by ID
    *   `DELETE`: Delete a specific unicorn by ID
*   Endpoint: `/unicorns/search?query`
    *   `GET`: Retrieve a list of unicorns filtered by `query`

This example defines 3 endpoints for the unicorn application:

*   The first endpoint `/unicorns` allows for `GET` operation to retrieve all the unicorns and `POST` to create a new unicorn
*   The second endpoint `/unicorns/{id}` allows for `GET` operation to retrieve a specific unicorn by ID, `PUT` operation to update a specific unicorn by ID, and `DELETE` operation to delete a specific unicorn by ID

The endpoints are defined using the standard HTTP methods (GET, POST, PUT/PATCH, DELETE) which are mapped to the CRUD operations(Create, Read, Update, Delete) respectively.

## Unicorns ~~Array~~ DB
Use the following array as a *data store* for your unicorns. Populate the array elements as documents in a mongodb. Host your MongoDB on MongoDB Atlas.
```js
 [
  {
    "_id": "6324fbe4998cf52fe226fb96",
    "name": "Horny",
    "dob": "1992-03-13T15:47:00.000Z",
    "loves": [
      "carrot",
      "papaya"
    ],
    "weight": 600,
    "gender": "m",
    "vampires": 63
  },
  {
    "_id": "6324fbe4998cf52fe226fb97",
    "name": "Aurora",
    "dob": "1991-01-24T21:00:00.000Z",
    "loves": [
      "carrot",
      "grape"
    ],
    "weight": 450,
    "gender": "f",
    "vampires": 43
  },
  {
    "_id": "6324fbe4998cf52fe226fb98",
    "name": "Unicrom",
    "dob": "1973-02-10T06:10:00.000Z",
    "loves": [
      "energon",
      "redbull"
    ],
    "weight": 984,
    "gender": "m",
    "vampires": 182
  },
  {
    "_id": "6324fbe4998cf52fe226fb99",
    "name": "Roooooodles",
    "dob": "1979-08-19T01:44:00.000Z",
    "loves": [
      "apple"
    ],
    "weight": 591,
    "gender": "m",
    "vampires": 99
  },
  {
    "_id": "6324fbe4998cf52fe226fb9a",
    "name": "Solnara",
    "dob": "1985-07-04T09:01:00.000Z",
    "loves": [
      "apple",
      "carrot",
      "chocolate"
    ],
    "weight": 550,
    "gender": "f",
    "vampires": 80
  },
  {
    "_id": "6324fbe4998cf52fe226fb9b",
    "name": "Ayna",
    "dob": "1998-03-07T16:30:00.000Z",
    "loves": [
      "strawberry",
      "lemon"
    ],
    "weight": 733,
    "gender": "f",
    "vampires": 40
  },
  {
    "_id": "6324fbe4998cf52fe226fb9c",
    "name": "Kenny",
    "dob": "1997-07-01T17:42:00.000Z",
    "loves": [
      "grape",
      "lemon"
    ],
    "weight": 690,
    "gender": "m",
    "vampires": 39
  },
  {
    "_id": "6324fbe4998cf52fe226fb9d",
    "name": "Raleigh",
    "dob": "2005-05-03T07:57:00.000Z",
    "loves": [
      "apple",
      "sugar"
    ],
    "weight": 421,
    "gender": "m",
    "vampires": 2
  },
  {
    "_id": "6324fbe4998cf52fe226fb9e",
    "name": "Leia",
    "dob": "2001-10-08T21:53:00.000Z",
    "loves": [
      "apple",
      "watermelon"
    ],
    "weight": 601,
    "gender": "f",
    "vampires": 33
  },
  {
    "_id": "6324fbe4998cf52fe226fb9f",
    "name": "Pilot",
    "dob": "1997-03-01T13:03:00.000Z",
    "loves": [
      "apple",
      "watermelon"
    ],
    "weight": 650,
    "gender": "m",
    "vampires": 54
  },
  {
    "_id": "6324fbe4998cf52fe226fba0",
    "name": "Nimue",
    "dob": "1999-12-21T00:15:00.000Z",
    "loves": [
      "grape",
      "carrot"
    ],
    "weight": 540,
    "gender": "f"
  },
  {
    "_id": "6324fbe5998cf52fe226fba1",
    "name": "Dunx",
    "dob": "1976-07-19T01:18:00.000Z",
    "loves": [
      "grape",
      "watermelon"
    ],
    "weight": 704,
    "gender": "m",
    "vampires": 165
  }
]
```

<!-- ## Development Strategy and Hints -->

# Testing 
Import `thunder-collection_Unicorns Test.json` into Thunder Client and run the tests.

You may also write your own requests in REST client extension or create the requests using POSTMAN.

# Challenges
<!-- Expand the labwork to read and write unicorns from/into files? 
Hint: Use the `fs` module and `JSON.stringify()` and `json.parse()`! -->

# Deliverables
Pass the Thunder Client tests, commit, and push.
