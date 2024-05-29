---
tags:
  - module
lecture_count: "15"
current_lecture: "4"
length: 3hr 17min
status: Ongoing
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13729276#content
module_number: 12
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [ ] [[#Authentication]]
	- [ ] [[#Securing Routes with JSON Web Tokens]]
- [x] [[#Password Encryption (bcrypt)]]
- [ ] Data Relationships (FK?)

```

## Password Encryption (bcrypt)
---

```bash
npm i bcryptjs
```

bcryptjs allows us to easily hash plain-text passwords.

```js
const bcrypt = require("bcryptjs");

const myFunction = async () => {
  const password = "password";
  const hashedPassword = await bcrypt.hash(password, 8);

  console.log(password, hashedPassword);
};

myFunction();

// password -> $2a$08$mlU.zd.WhU5xZUJNUSuhquOkhdp8Rcp2ApKUBYGbzRU9C6uzOcWaC
```

```ad-warning
title: hashing is *one* way - you can't un-hash a string!
```

In order to *validate* a hashed password, we can hash the plain-text provided when logging in and we compare that hash with the has stored in the database. 

```js
const bcrypt = require("bcryptjs");

const myFunction = async () => {
  const password = "password";
  const hashedPassword = await bcrypt.hash(password, 8);

  console.log(password, hashedPassword);

  // password -> true
  // Password -> false
  const isMatch = await bcrypt.compare("password", hashedPassword);
  console.log(isMatch);
};

myFunction();
```

Instead of directly validating our passwords from within the Express routes, we'll use middleware with our Mongoose Model's to further separate our concerns. 

| Application        | Concern                                     |
| ------------------ | ------------------------------------------- |
| User Route      -> | - Create<br>- Read<br>- Update <br>- Delete |
| User Model      -> | - Define User Properties                    |
| User Middleware -> | - Validate Incoming Requests                |

To apply middleware, we'll use the built-in Mongoose Schema methods. Middleware functions in Mongoose are executed at various stages of the document lifecycle, allowing us to run functions before (`pre`) or after (`post`) certain actions (e.g., saving a document).

```js
const mongoose = require("mongoose");
const validator = require("validator");

const userSchema = new mongoose.Schema({
  // ...
});

userSchema.pre("save", async function (next) {
  const user = this;

  // Created for the first time || being updated -> true
  if (user.isModified("password")) {
    user.password = await bcrypt.hash(user.password, 8);
  }

  next(); // Signal you're done + continue
});

const User = mongoose.model("User", userSchema);

module.exports = User;

```

`isModified`
	It returns `true` if the *field* has been modified since the document was retrieved from the database (created or updated), and `false` otherwise.


````ad-warning
title: Not all functions call the `save` method

When validating using middleware, it's important to know which CRUD operations you're actually affecting. 

If you wanted this middleware function to also apply to your `update` function,  you'll have to update the user by directly mutating the object and calling the `save` function like so:

```js
// Update User
router.patch("/users/:id", async (req, res) => {
  const updates = Object.keys(req.body);
  const fields = ["name", "email", "password", "age"];
  const validOperation = updates.every((update) => fields.includes(update));

  if (!validOperation) {
    return res.status(400).send({ error: "Invalid updates" });
  }

  try {
    const updatedUser = await User.findById(req.params.id);

    updates.forEach(
      (updateField) => (updatedUser[updateField] = req.body[updateField])
    );

    await updatedUser.save(); // triggers middleware

    if (!updatedUser) {
      return res.status(404).send();
    }

    res.send(updatedUser);
  } catch (e) {
    res.status(400).send(e);
  }
});
```

````


## Authentication
---

In order to authenticate our Users, we need to do 2 things:

1. Verify that the provided `email` exists with an associated User
2. Compare the provided plain-text password with the encrypted password from the found User

Mongoose allows us to define custom functions through a defined schema with a `statics` property with the following syntax:

```
schema.statics.customFunctionName = async () => { }
```


`````ad-seealso
title: What is the `statics` property?
collapse: 

The `statics` property is used to define static methods for your model. Static methods are functions that you can call directly on the model itself, tather than on an instance of the model. These methods are typically used for operations that are not specific to a single document, such as custom queries or utility functions related to the entire collection of documents.

`````

#### Ex.
```js
// Find w/ credentials
userSchema.statics.findByCredentials = async (email, password) => {
  const user = await User.findOne({ email });

  if (!user) {
    throw new Error("Unable to login");
  }

  const isMatch = await bcrypt.compare(password, user.password);

  if (!isMatch) {
    throw new Error("Unable to login");
  }

  return user;
};
```


---


Now that we have a way to validate an incoming request body, we just need to create a route to execute it with.

```js
// Log in user
router.post("/users/login", async (req, res) => {
  try {
    const user = await User.findByCredentials(
      req.body.email,
      req.body.password
    );
    res.send(user);
  } catch (e) {
    res.status(400).send();
  }
});
```

```ad-question
title: Why do we use `POST` instead of `GET`? 

Quickread: [[HTTP#Methods]]

TLDR:
- **GET**: Used to retrieve data from the server. It should not have any side effects.
- **POST**: Used to submit data to the server, often causing a change in state or side effects on the server.

Since logging in involves sending sensitive information (such as a username and password) to the server to authenticate the user and potentially create a session, it is considered an operation that can cause side effects. Therefore, it fits the semantics of a `POST` request rather than a `GET` request.

```


#### Securing Routes with JSON Web Tokens
---

```ad-seealso

- [[JSON Web Tokens]]

```


From here, we'll be using the library [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken) for a simple way to interact with JWT's.

```bash
npm i jsonwebtoken
```

```js
const jwt = require("jsonwebtoken");
```

For most cases, you'll be using only 2 functions in order to create and validate the tokens:

1. `jwt.sign({}, "", {}) -> jwt`
2. `jwt.verify("", "") -> bool`

```js
const jwt = require('jsonwebtoken');

// Secret key for signing the token
// Usually stored in a .env file
const secretKey = 'your-very-secret-key';

// Data to include in the JWT payload
const payload = {
  userId: '1234567890',
  name: 'John Doe',
  admin: true
};

// Options for the token
const options = {
  expiresIn: '1h' // The token will expire in 1 hour
};

// Create (sign) the token
const token = jwt.sign(payload, secretKey, options);

console.log('Signed JWT:', token);

// Verify and decode the token
const data = jwt.verify(token, secretKey);

console.log(data);
```


Despite the JWT seeming gibberish, it's clearly separated into 3 parts with periods. The *header*, *payload*, and *signature* respectively.

To verify this, you can copy the middle payload into a [Base64 Decoder](https://www.base64decode.org/) to view the data being passed. 
#### JWT Output
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiIxMjM0NSIsImlhdCI6MTcxNjU3ODc1NSwiZXhwIjoxNzE2NjY1MTU1fQ.12oDmBAIyIw6wmnvMLT-p2N3xLtNWn_sg0wpkkwZdg0
```


```ad-tip
title: Tracking JWT's
collapse:

A common practice to track JWT's for a User is to add a `tokens: [ { } ]` field to the model. This way, each token created by a user can be tracked from within the array.

```






---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
