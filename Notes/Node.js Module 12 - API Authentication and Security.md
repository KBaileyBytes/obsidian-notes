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

- [ ] Authentication
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



---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
