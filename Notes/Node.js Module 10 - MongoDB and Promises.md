---
tags:
  - module
lecture_count: "12"
current_lecture: "12"
length: 2hr 23min
status: Complete
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13729122#questions/11722552
module_number: 10
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] [[#Connect NodeJS to MongoDB]]
- [ ] User Authentication
- [ ] File Upload
- [ ] Email Notifications
- [x] [[#CRUD]]

```


`````ad-abstract
title: SQL vs NoSQL
collapse: 

**SQL (Structured Query Language)**

1. **Definition**: SQL is a standard language for managing relational databases. It is used to create, retrieve, update, and delete data in relational database management systems (RDBMS).
    
2. **Characteristics**:
    
    - Declarative: SQL allows users to specify what data they need without having to specify how to retrieve it.
    - Data Manipulation Language (DML): SQL supports operations such as INSERT, UPDATE, DELETE, and SELECT for manipulating data.
    - Data Definition Language (DDL): SQL allows defining and modifying the structure of database objects like tables, indexes, etc.
    - Data Control Language (DCL): SQL provides commands to control access to data within the database.
    - Transaction Control Language (TCL): SQL supports commands for managing transactions.
3. **Relational Databases**: SQL is primarily used with relational databases, where data is organized into tables with rows and columns. It enforces ACID (Atomicity, Consistency, Isolation, Durability) properties to maintain data integrity.
    
4. **Examples of SQL RDBMS**: MySQL, PostgreSQL, SQLite, Oracle Database, Microsoft SQL Server.
    
5. **Use Cases**:
    
    - Traditional business applications
    - Financial systems
    - Human Resources Management Systems (HRMS)
    - Content Management Systems (CMS)
    - E-commerce applications

**NoSQL (Not Only SQL)**

1. **Definition**: NoSQL encompasses a wide range of database technologies that were developed as an alternative to traditional SQL databases. NoSQL databases are designed to handle large volumes of unstructured, semi-structured, and structured data.
    
2. **Characteristics**:
    
    - Schema-less: NoSQL databases typically do not require a fixed schema, allowing for flexibility in data models.
    - Distributed: Many NoSQL databases are designed to scale horizontally across multiple nodes, providing high availability and fault tolerance.
    - Non-relational: NoSQL databases may use various data models, such as key-value, document, columnar, or graph.
    - Eventually Consistent: Some NoSQL databases prioritize availability and partition tolerance over strict consistency, providing eventual consistency guarantees.
3. **Types of NoSQL Databases**:
    
    - **Key-Value Stores**: Data is stored as a collection of key-value pairs. Example: Redis, DynamoDB.
    - **Document Stores**: Data is stored as documents (e.g., JSON, XML) with a flexible schema. Example: MongoDB, Couchbase.
    - **Column-Family Stores**: Data is stored in columns grouped by column families. Example: Apache Cassandra, HBase.
    - **Graph Databases**: Data is stored as nodes and edges to represent complex relationships. Example: Neo4j, Amazon Neptune.
4. **Use Cases**:
    
    - Big data and real-time analytics
    - Content management and delivery
    - IoT (Internet of Things) applications
    - Social media analytics
    - Gaming applications
5. **Challenges**:
    
    - Lack of standardized query language (each NoSQL database may have its own query interface).
    - Limited ACID compliance compared to traditional SQL databases.
    - Data consistency may be sacrificed for scalability and performance.
    - Learning curve for developers accustomed to SQL databases.


<br>

```ad-tip
title: SQL

![[Pasted image 20240327104334.png | center]]
```

<br>

```ad-tip
title: NoSQL

![[Pasted image 20240327104354.png | center]]
```

`````


```ad-tip
title: MongoDB Overview

## What is MongoDB?

MongoDB is a popular open-source NoSQL database that provides high performance, high availability, and easy scalability. It stores data in flexible, JSON-like documents, making it suitable for a wide range of applications.

## Key Features:

- **Flexible Schema**: MongoDB's document model allows for dynamic and flexible schemas, making it easy to evolve data structures over time.
- **High Performance**: MongoDB is designed for high performance, with support for indexing, sharding, and replication.
- **Horizontal Scalability**: MongoDB can scale horizontally across multiple servers to handle large volumes of data and high throughput.
- **Rich Query Language**: MongoDB supports a powerful query language with support for complex queries, aggregation, and indexing.
- **Built-in Replication and Failover**: MongoDB provides built-in replication and failover capabilities for high availability and data durability.
- **Ease of Use**: MongoDB is easy to install, configure, and use, with a rich set of APIs and drivers for popular programming languages.
```

````ad-abstract
title: What is ObjectID?
collapse:

`ObjectID` is a unique identifier assigned to each document within a collection. It is automatically generated by MongoDB for every document inserted into a collection if the document does not already contain an `_id` field.

|Method|Definition|Parameters|Notes|
|---|---|---|---|
|`ObjectId()`|Creates a new `ObjectID` instance.|None|None|
|`ObjectId.isValid()`|Checks if the provided string is a valid `ObjectID`.|`id` (string): The string to validate.|This method can be used to validate whether a given string is a valid `ObjectID` before using it in MongoDB operations.|
|`ObjectId.getTimestamp()`|Returns the timestamp portion of the `ObjectID`, representing the creation time of the document.|None|The returned timestamp is a `Date` object.|
|`ObjectId.equals()`|Compares two `ObjectID` instances for equality.|`otherId` (ObjectId): The `ObjectID` to compare against.|This method is useful for comparing `ObjectID`s when performing operations like filtering or sorting documents.|
|`ObjectId.toHexString()`|Returns the hexadecimal string representation of the `ObjectID`.|None|This method converts the `ObjectID` to its hexadecimal string representation, which can be useful for logging or display purposes.|
|`ObjectId.toString()`|Returns the string representation of the `ObjectID`.|None|This method returns the `ObjectID` as a string.|
|`ObjectId.createFromTime()`|Creates an `ObjectID` with a specific timestamp.|`time` (number): The Unix timestamp in seconds.|Useful for creating `ObjectID`s with a custom timestamp.|
|`ObjectId.createFromHexString()`|Creates an `ObjectID` from a hexadecimal string representation.|`hexString` (string): The hexadecimal string.|Useful when you have a hexadecimal string and need to create an `ObjectID` instance from it.|

````


# MongoDB Community Server
---

## What is MongoDB Community Server?

MongoDB Community Server is the free and open-source version of MongoDB. It provides all the core features of MongoDB, including document storage, [[indexing]], [[replication]], and [[sharding]]. MongoDB Community Server is suitable for small to medium-sized projects and is widely used by developers and organizations around the world.

With the MongoDB Community Server installed, you can run the following command to start the MongoDB server:

```bash
/Users/Bromo/mongodb/bin/mongod.exe --dbpath=/Users/Bromo/mongodb-data
```

## Connecting to MongoDB

To connect to a MongoDB database from your Node.js application, you'll need to create a MongoClient object and specify the connection URL:

```js
const { MongoClient } = require('mongodb');
// or as an es module:
// import { MongoClient } from 'mongodb'

const connectionURL = "mongodb://127.0.0.1:27017";
const client = new MongoClient(connectionURL);

async function main() {
  await client.connect();
  console.log("Successfully connected to the server.");
  const db = client.db("task-manager");
  // const users = db.collection("users"); or some other table

  return "Operations complete.";
}

main()
  .then(console.log)
  .catch(console.error)
  .finally(() => client.close());

```

## CRUD

| Method                       | Definition                                                                                                                                                                    | Example                                                                     |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `db.collection.insertOne()`  | Inserts a single document into a collection.                                                                                                                                  | `users.insertOne({ name: "John", age: 30 })`                                |
| `db.collection.insertMany()` | Inserts multiple documents into a collection.                                                                                                                                 | `users.insertMany([{ name: "John", age: 30 }, { name: "Alice", age: 25 }])` |
| `db.collection.find()`       | Retrieves documents from a collection based on specified criteria.                                                                                                            | `users.find({ age: { $gte: 25 } })`                                         |
| `db.collection.findOne()`    | Retrieves a single document from a collection based on specified criteria.                                                                                                    | `users.findOne({ name: "John" })`                                           |
| `db.collection.updateOne()`  | Updates a single document within a collection that matches specified criteria.                                                                                                | `users.updateOne({ name: "John" }, { $set: { age: 32 } })`                  |
| `db.collection.updateMany()` | Updates multiple documents within a collection that match specified criteria.                                                                                                 | `users.updateMany({ age: { $gte: 30 } }, { $inc: { age: 1 } })`             |
| `db.collection.replaceOne()` | Replaces a single document within a collection that matches specified criteria with a new document.                                                                           | `users.replaceOne({ name: "John" }, { name: "John Doe", age: 35 })`         |
| `db.collection.deleteOne()`  | Deletes a single document from a collection based on specified criteria.                                                                                                      | `users.deleteOne({ name: "John" })`                                         |
| `db.collection.deleteMany()` | Deletes multiple documents from a collection based on specified criteria.                                                                                                     | `users.deleteMany({ age: { $lt: 25 } })`                                    |
| `db.collection.aggregate()`  | Performs aggregation operations on the documents of a collection. Aggregation operations process data records and return computed results.                                    | `users.aggregate([{ $group: { _id: "$age", count: { $sum: 1 } } }])`        |
| `db.collection.bulkWrite()`  | Executes a series of write operations, such as insert, update, replace, or delete, across one or more collections. This can improve performance by reducing network overhead. | `users.bulkWrite([{ insertOne: { document: { name: "Jane", age: 28 } } }])` |

```ad-abstract
title: Update Operators

|Operator|Description|Example|
|---|---|---|
|`$set`|Sets the value of a field in a document. If the field does not exist, `$set` creates it.|`db.collection.updateOne({ _id: ObjectId("123456") }, { $set: { "field": "value" } })`|
|`$unset`|Removes the specified field from a document.|`db.collection.updateOne({ _id: ObjectId("123456") }, { $unset: { "field": "" } })`|
|`$inc`|Increments the value of a field by a specified amount. If the field does not exist, `$inc` sets it to the specified amount.|`db.collection.updateOne({ _id: ObjectId("123456") }, { $inc: { "field": 5 } })`|
|`$push`|Appends a specified value to an array field. If the field is absent in the document, `$push` creates it as an array.|`db.collection.updateOne({ _id: ObjectId("123456") }, { $push: { "field": "value" } })`|
|`$addToSet`|Adds a value to an array field only if it is not already present. If the field is absent in the document, `$addToSet` creates it as an array.|`db.collection.updateOne({ _id: ObjectId("123456") }, { $addToSet: { "field": "value" } })`|
|`$pull`|Removes all instances of a specified value from an array field.|`db.collection.updateOne({ _id: ObjectId("123456") }, { $pull: { "field": "value" } })`|
|`$rename`|Renames a field in a document.|`db.collection.updateOne({ _id: ObjectId("123456") }, { $rename: { "oldField": "newField" } })`|
|`$currentDate`|Sets the value of a field to the current date either as a Date or a Timestamp.|`db.collection.updateOne({ _id: ObjectId("123456") }, { $currentDate: { "lastModified": true } })`|
|`$addToSet`|Adds elements to an array field only if they do not already exist in the set.|`db.collection.updateOne({ _id: ObjectId("123456") }, { $addToSet: { "field": { $each: ["value1", "value2"] } } })`|
```


---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
