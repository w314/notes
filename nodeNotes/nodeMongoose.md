# Mongoose
> It is an object data model (ODM) library used for creating schemas which is later mapped to MongoDB documents.

- works in an asynchoronous MongoDB environment
- imposes the structure and constraints of the database by mapping JS objects to MongoDB documents

Functionality
- validating field values
- methods for
    - select
    - modify
    - add
    - delete records

Sources:
- [Geeks for Geeks](https://www.geeksforgeeks.org/mongoose-vs-mongodb/)


## Schema

Describes the structure of the document to be inserted.

Allows us to:
- perform validations
- provide default values


## `Model` method

Helps with interacting with the database, takes a schema and creates a document. Provides and interface to the database.


## Working with Mongoose

### 1. Install mongoose

`npm install --save mongoose`

### 2. Connect to the database

To start MongoDB with Compass:
- open compass
- click `+ Add new connection`
- click `save and connect`

```js
```

### #. Create a Schema and model
- create schema/model for each schema that is needed



```js
const { Schema, model } = mongoose;


### 3. Create a collection
the first argument passed to the model should be the singular form of your collection name. Mongoose automatically changes this to the plural form, transforms it to lowercase, and uses that for the database collection name.
