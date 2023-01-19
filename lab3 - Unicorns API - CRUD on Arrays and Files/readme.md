To be submitted during lab hours


# Intro - CRUD on Arrays and Files
CRUD stands for Create, Read, Update, and Delete, which are the four basic operations of persistent storage.

To perform CRUD operations on a JavaScript array, you can use the following methods:

Create:

*   `array.push(element)` adds an element to the end of an array.
*   `array.unshift(element)` adds an element to the beginning of an array.

Read:

*   `array[index]` retrieves the element at a given index.
*   `array.slice(start, end)` retrieves a section of an array.
*   `array.forEach(function)` iterates over an array and applies a function to each element.

Update:

*   `array[index] = element` updates the element at a given index.
*   `array.splice(index, numberOfElements, element)` removes a number of elements from an array starting at a given index and replaces them with a new element.

Delete:

*   `array.pop()` removes the last element of an array.
*   `array.shift()` removes the first element of an array.
*   `array.splice(index, numberOfElements)` removes a number of elements from an array starting at a given index.

Example:

```js

let arr = ["apple", "banana", "orange"]

// Create
arr.push("mango");
console.log(arr); // ["apple", "banana", "orange", "mango"]

// Read
console.log(arr[1]); // "banana"
console.log(arr.slice(1, 3)); // ["banana", "orange"]
arr.forEach(function(element) { console.log(element); });

// Update
arr[1] = "kiwi";
console.log(arr); // ["apple", "kiwi", "orange", "mango"]
arr.splice(1, 1, "pear");
console.log(arr); // ["apple", "pear", "orange", "mango"]

// Delete
arr.pop();
console.log(arr); // ["apple", "pear", "orange"]
arr.shift();
console.log(arr); // ["pear", "orange"]
arr.splice(0, 2);
console.log(arr); // []
```

# CRUD on JS Arrays
To mimic CRUD operations on a JavaScript array of objects that mimics a MongoDB collection, you can use the following methods:

Create:

*   `array.push(object)` adds an object to the end of an array.

Read:

*   `array.find(function)` returns the first object in the array that satisfies a given condition.
*   `array.filter(function)` returns an array of all objects that satisfy a given condition.
*   `array.forEach(function)` iterates over an array and applies a function to each object.

Update:

*   `array.map(function)` iterates over an array and returns a new array with the results of applying a function to each object.

Delete:

*   `array.filter(function)` returns an array of all objects that do not satisfy a given condition.

Example:


```js
let collection = [
    { _id: 1, name: "John", age: 30 },
    { _id: 2, name: "Jane", age: 25 },
    { _id: 3, name: "Bob", age: 35 }
];

// Create
let newDoc = { _id: 4, name: "Emily", age: 22 };
collection.push(newDoc);
console.log(collection); 
/*
[
    { _id: 1, name: "John", age: 30 },
    { _id: 2, name: "Jane", age: 25 },
    { _id: 3, name: "Bob", age: 35 },
    { _id: 4, name: "Emily", age: 22 }
]
*/

// Read
console.log(collection.find(doc => doc._id === 2)); // { _id: 2, name: "Jane", age: 25 }
console.log(collection.filter(doc => doc.age > 30));
/*
[
    { _id: 3, name: "Bob", age: 35 }
]
*/
collection.forEach(function(doc) { console.log(doc); });

// Update
collection = collection.map(doc => {
  if (doc._id === 3) {
    return { ...doc, age: 40 };
  }
  return doc;
});
console.log(collection);
/*
[
    { _id: 1, name: "John", age: 30 },
    { _id: 2, name: "Jane", age: 25 },
    { _id: 3, name: "Bob", age: 40 },
    { _id: 4, name: "Emily", age: 22 }
]
*/

// Delete
collection = collection.filter(doc => doc._id !== 4);
console.log(collection);
/*
[
    { _id: 1, name: "John", age: 30 },
    { _id: 2, name: "Jane", age: 25 },
    { _id: 3, name: "Bob", age: 40 }
]
*/

```

# More Fun with JS arrays
Sort:

*   `array.sort(compareFunction)` sorts the elements of an array according to a compare function.

Skip:

*   `array.slice(start, end)` retrieves a section of an array, skipping the first 'start' elements and returning the next 'end' elements.

Count:

*   `array.length` returns the number of elements in an array.

Example:


```js
let collection = [
    { _id: 1, name: "John", age: 30 },
    { _id: 2, name: "Jane", age: 25 },
    { _id: 3, name: "Bob", age: 35 }
];

// Sort
collection.sort((a, b) => (a.age > b.age) ? 1 : -1);
console.log(collection); 
/*
[
    { _id: 2, name: "Jane", age: 25 },
    { _id: 1, name: "John", age: 30 },
    { _id: 3, name: "Bob", age: 35 }
]
*/

// Skip
let skipped = collection.slice(1, 3);
console.log(skipped); 
/*
[
    { _id: 1, name: "John", age: 30 },
    { _id: 3, name: "Bob", age: 35 }
]
*/

// Count
console.log(collection.length); // 3
```

You can also use some functional programming helper libraries like `lodash` or `ramda` that have their own sorting, filtering, and mapping functions. These libraries provide a more efficient, expressive, and easier to use way to perform the same operations on an array of objects.

Example with Lodash:

```js
let collection = [
    { _id: 1, name: "John", age: 30 },
    { _id: 2, name: "Jane", age: 25 },
    { _id: 3, name: "Bob", age: 35 }
];

// Sort
let sorted = _.sortBy(collection, "age");
console.log(sorted);

//Skip
let skip = _.slice(sorted, 1, 3);
console.log(skip);

//Count
console.log(_.size(collection));

```



# Lab 3 - Unicorns API - V1 🦄
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
*   The third endpoint `/unicorns/search?query` allows for `GET` operation to retrieve a list of unicorns filtered by a query

The endpoints are defined using the standard HTTP methods (GET, POST, PUT, DELETE) which are mapped to the CRUD operations(Create, Read, Update, Delete) respectively.

## Unicorns Array
Use the following array as a *data store* for your unicorns.
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

## More Endpoints (Optional)
Let us try to implement an API that would be able to resolve these client queried requests:
- Q1 Find the male unicorns weigh  more than 700 pounds
- Q3 Find the unicorns that like apples 


### More Endpoints Specification
- Endpoint: `/unicorns/search?gender={gender}&weight={weight}`
    *   `GET`: Retrieve a list of unicorns filtered by gender and weight

The endpoint `/unicorns/search?gender={gender}&weight={weight}` allows for `GET` operation to retrieve a list of unicorns filtered by gender and weight. It uses two query parameters `gender` and `weight` for filtering. This endpoint allows you to retrieve a list of unicorns of a specific gender (male or female) that weigh more than a specific weight.

Example:

*   `GET /unicorns/search?gender=male&weight=600` returns a list of all male unicorns that weigh more than 600.
*   `GET /unicorns/search?gender=female&weight=500` returns a list of all female unicorns that weigh more than 500.

---


*   Endpoint: `/unicorns/search?food={food}`
    *   `GET`: Retrieve a list of unicorns filtered by food preference

The endpoint `/unicorns/search?food={food}` allows for `GET` operation to retrieve a list of unicorns filtered by their food preference. it uses a query parameter `food` for filtering. This endpoint allows you to retrieve a list of unicorns that like a specific food item.

Example:

*   `GET /unicorns/search?food=hay` returns a list of all unicorns that like hay as food.
*   `GET /unicorns/search?food=apples` returns a list of all unicorns that like apples as food.

# Testing 
## Option I - Unit Testing
You may use unit tests in the `__test__` folder. To run them use
```
npm test
```
in your vscode terminal 

## Optional II
Import"thunder-collection_Unicorns Test.json" into Thunder Client and run the tests.

You may also write your own requests in REST client extension or create the requests using POSTMAN.

# Challenges
Expand the labwork to read and write unicorns from/into files? 
Hint: Use the `fs` module and `JSON.stringify()` and `json.parse()`!

# Deliverables
Pass the tests, commit, and push.
