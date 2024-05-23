---
tags:
  - module
lecture_count: "20"
current_lecture: "20"
length: 4hr 8min
status: Complete
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13729172#questions/11722552
module_number: 11
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] [[#Creating a REST API]]
- [x] Mongoose Basics
- [x] Express Routers

```

``````ad-seealso
title: See Also...

- [[Model and Schema Naming Conventions]]
- [[Basic Mongoose Validation]]
``````


``````ad-abstract
title: What is Mongoose?


## Mongoose

Mongoose is an Object Document Mapper ([[ODM vs ORM | ODM]]) library for MongoDB and Node.js. It provides a straightforward, schema-based solution to model application data. Mongoose translates data in the MongoDB database to JavaScript objects for use in your application and vice versa.

### Features of Mongoose:

- **Schema Definition**: Mongoose allows you to define schemas for your data models. Schemas define the structure of documents within a collection and enforce data validation.
  
- **Modeling Relationships**: You can define relationships between data models using Mongoose. This enables you to create complex data structures and easily navigate between related documents.
  
- **Middleware**: Mongoose supports middleware functions that can intercept and modify data before or after certain operations (e.g., saving a document, querying data).
  
- **Query Building**: Mongoose provides a fluent API for building complex queries. This makes it easy to retrieve and manipulate data from MongoDB.
  
- **Validation and Sanitization**: Mongoose allows you to define validation rules for your schema fields, ensuring that data conforms to your expectations. It also provides built-in support for sanitizing data to prevent injection attacks and other security vulnerabilities.

<br>

### Validation and Sanitization with Mongoose:

Mongoose offers several ways to perform validation and sanitization:

- **Schema Validators**: You can define validators for schema fields using built-in validation rules or custom functions. Validators enforce data integrity by validating input before saving it to the database.
  
- **Custom Validators**: Mongoose allows you to define custom validation logic using functions. This gives you fine-grained control over the validation process and allows you to enforce business-specific rules.
  
- **Built-in Sanitizers**: Mongoose provides built-in sanitization functions for common data types (e.g., strings, numbers). These sanitizers automatically clean input data to prevent injection attacks and other security vulnerabilities.
  
- **Middleware**: Mongoose middleware functions can be used for additional validation and sanitization tasks. Middleware functions are executed before or after certain operations, allowing you to modify data as needed.

Mongoose's validation and sanitization features help ensure data integrity and security in MongoDB applications, making it a powerful tool for building robust and secure systems.


``````

`````ad-question
title: What is the difference between a Schema and a Model?
collapse: 

Models represent collections or tables in your MongoDB database. A Schema defines the structure of the documents **within** a collection. 

Collection of cakes -> recipe for the cake

`````


# Creating a REST API
---

***REST API*** - Representational State Transfer - Application Programming Interface
	- aka. RESTful API or REST API

A RESTful API is a type of web service that follows the principles of REST architectural style. It allows different computer systems to communicate over [[HTTP]] in a simple, standardized way. REST APIs are commonly used for building web services that are scalable, maintainable, and interoperable.

**REST (Representational State Transfer):** REST is an architectural style for designing networked applications. It stands for Representational State Transfer. RESTful systems typically use HTTP requests to perform ***CRUD*** (Create, Read, Update, Delete) operations on resources.

**API (Application Programming Interface):** An API is a set of rules, protocols, and tools that allows different software applications to communicate with each other. APIs define the methods and data formats that developers can use to interact with a service or application, abstracting away the underlying implementation details. APIs can be used to access web services, databases, operating systems, and other software components.


````ad-abstract
title: Key Principles of REST API
collapse:

1. **Stateless**: Each request from a client to the server must contain all the information necessary to understand and fulfill the request. The server should not store any client context between requests.

2. **Uniform Interface**: REST APIs should have a uniform interface, typically consisting of resources identified by URIs, standard HTTP methods (GET, POST, PUT, DELETE), and standard media types (e.g., JSON, XML) for representing resource representations.

3. **Client-Server Architecture**: The client and server should be independent of each other, allowing them to evolve separately over time. This separation improves scalability by allowing the components to be developed and deployed independently.

4. **Cacheable**: Responses from the server should be explicitly or implicitly labeled as cacheable or non-cacheable. This improves performance and scalability by reducing the need for repeated requests to the server.

5. **Layered System**: REST APIs can be built in a layered architecture, where each layer has a specific responsibility. This promotes separation of concerns and allows for scalability and security enhancements.

````


````ad-abstract
title: Using Router to Simplify `index.js`

# Express Router Overview and Use Cases

## Overview

Express Router is a middleware that allows you to modularize your Express application's routes into separate files or modules. It provides a cleaner and more organized way to handle routes and middleware within your application.

By using the Router function, you can define multiple routes within a single file and then mount this router on a specific route path in your main Express application. This makes your code more maintainable and easier to understand, especially as your application grows in complexity.

## Use Cases

1. **Modular Routing**: Router enables you to organize your routes into separate modules or files based on their functionality. This makes it easier to manage and maintain your codebase, especially for larger applications.

2. **Route Handling**: You can define route handlers for different HTTP methods (GET, POST, PUT, DELETE, etc.) within the Router instance. This allows you to encapsulate the logic for handling specific requests under different routes.

3. **Middleware Support**: Express Router supports middleware functions just like the main Express application. You can use middleware to perform tasks such as authentication, request validation, error handling, etc., specific to certain routes or groups of routes.

4. **Parameterized Routes**: Router supports parameterized routes, allowing you to define dynamic route paths that can capture values from the URL. This is useful for creating RESTful APIs where you need to work with resource identifiers or other dynamic values.

5. **Code Reusability**: By encapsulating related routes and middleware within a Router instance, you can easily reuse them across different parts of your application or even in multiple applications.

6. **Error Handling**: Router allows you to define error-handling middleware specific to certain routes or groups of routes. This enables you to customize error responses or perform specific actions based on the type of error encountered.

7. **Mounting Routers**: You can mount a Router instance on a specific route path in your main Express application using the `app.use()` method. This enables you to create modular and nested route structures within your application.

````


## Express Routing
---

Express routers allow you to break your application into smaller modules, each handling a specific part of your app's functionality. This can make your code more organized and maintainable:

```js
// users.js
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
    res.send('Users home');
});

router.get('/:id', (req, res) => {
    res.send(`User with ID ${req.params.id}`);
});

module.exports = router;

// main app
const express = require('express');
const app = express();
const usersRouter = require('./users');

app.use('/users', usersRouter);

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
