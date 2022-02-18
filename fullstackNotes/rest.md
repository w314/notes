rest

# REST
[more info](https://restfulapi.net/)

> A pattern for organizing API endpoints

REST (**RE**presentational **S**tate **T**ransfer) implies a specific set of API endpoints for every entity in the app.
There are 5 actionable RESTful routes for APIs
- INDEX 
    - /users -> GET
    - returns all of the items in a database table and all of their properties
- SHOW
    - /users:id -> GET
    - returns an object
- CREATE
    - /users -> POST
    - adds the object carried in the `POST` request as a new item to the database
    - usually returns a copy of the newly created item
- EDIT
    - /users:id -> PUT/PATCH
    - updates an item of the database
    - usually returns a copy of the updated item
- DELETE
    - /users:id -> DELETE
    - deletes the item
    - typically returns a copy of the deleted item
