---
tags:
  - note
Framework: Mongoose
---
# `= this.file.name `
---

Mongoose offers several ways to validate data before it is saved to the database. These include built-in validators, custom validators, and middleware hooks. Below are some common ways to perform validation with Mongoose:

`````ad-abstract
title: Mongoose SchemaTypes

- [String](https://mongoosejs.com/docs/schematypes.html#strings)
- [Number](https://mongoosejs.com/docs/schematypes.html#numbers)
- [Date](https://mongoosejs.com/docs/schematypes.html#dates)
- [Buffer](https://mongoosejs.com/docs/schematypes.html#buffers)
- [Boolean](https://mongoosejs.com/docs/schematypes.html#booleans)
- [Mixed](https://mongoosejs.com/docs/schematypes.html#mixed)
- [ObjectId](https://mongoosejs.com/docs/schematypes.html#objectids)
- [Array](https://mongoosejs.com/docs/schematypes.html#arrays)
- [Decimal128](https://mongoosejs.com/docs/api/mongoose.html#mongoose_Mongoose-Decimal128)
- [Map](https://mongoosejs.com/docs/schematypes.html#maps)
- [Schema](https://mongoosejs.com/docs/schematypes.html#schemas)
- [UUID](https://mongoosejs.com/docs/schematypes.html#uuid)
- [BigInt](https://mongoosejs.com/docs/schematypes.html#bigint)

````ad-example
title: More Schema Properties

- `required`: boolean or function, if true adds a [required validator](https://mongoosejs.com/docs/validation.html#built-in-validators) for this property
- `default`: Any or function, sets a default value for the path. If the value is a function, the return value of the function is used as the default.
- `select`: boolean, specifies default [projections](https://www.mongodb.com/docs/manual/tutorial/project-fields-from-query-results/) for queries
- `validate`: function, adds a [validator function](https://mongoosejs.com/docs/validation.html#built-in-validators) for this property
- `get`: function, defines a custom getter for this property using [`Object.defineProperty()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty).
- `set`: function, defines a custom setter for this property using [`Object.defineProperty()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty).
- `alias`: string, mongoose >= 4.10.0 only. Defines a [virtual](https://mongoosejs.com/docs/guide.html#virtuals) with the given name that gets/sets this path.
- `immutable`: boolean, defines path as immutable. Mongoose prevents you from changing immutable paths unless the parent document has `isNew: true`.
- `transform`: function, Mongoose calls this function when you call [`Document#toJSON()`](https://mongoosejs.com/docs/api/document.html#document_Document-toJSON) function, including when you [`JSON.stringify()`](https://thecodebarbarian.com/the-80-20-guide-to-json-stringify-in-javascript) a document.

```javascript
const numberSchema = new Schema({
  integerOnly: {
    type: Number,
    get: v => Math.round(v),
    set: v => Math.round(v),
    alias: 'i'
  }
});

const Number = mongoose.model('Number', numberSchema);

const doc = new Number();
doc.integerOnly = 2.001;
doc.integerOnly; // 2
doc.i; // 2
doc.i = 3.001;
doc.integerOnly; // 3
doc.i; // 3
```

````


`````


1. **Built-in Validators**:
	- Mongoose provides a range of built-in validators for common data types such as strings, numbers, dates, and arrays.
	- Validation is defined in the [SchemaType](https://mongoosejs.com/docs/schematypes.html)
	- Validation is [middleware](https://mongoosejs.com/docs/middleware.html). Mongoose registers validation as a `pre('save')` hook on every schema by default.
	- Validation always runs as the **first** `pre('save')` hook. This means that validation doesn't run on any changes you make in `pre('save')` hooks.
	- You can disable automatic validation before save by setting the [validateBeforeSave](https://mongoosejs.com/docs/guide.html#validateBeforeSave) option
	- You can manually run validation using `doc.validate()` or `doc.validateSync()`
	- You can manually mark a field as invalid (causing validation to fail) by using [`doc.invalidate(...)`](https://mongoosejs.com/docs/api/document.html#document_Document-invalidate)
	- Validators are not run on undefined values. The only exception is the [`required` validator](https://mongoosejs.com/docs/api/schematype.html#schematype_SchemaType-required).
	- Example:

```js 
const userSchema = new mongoose.Schema({
    username: {
        type: String,
        required: true,
        minlength: 3,
        maxlength: 20
    },
    email: {
        type: String,
        required: true,
        unique: true,
        match: /^\S+@\S+\.\S+$/
    },
    age: {
        type: Number,
        min: 18
    }
});
```

- **Custom Validators**:
    - You can define custom validation functions to perform complex validation logic.
    - Example:

```js
function validatePhone(phone) {
    return /^\d{10}$/.test(phone);
}

const userSchema = new mongoose.Schema({
    phone: {
        type: String,
        validate: [validatePhone, 'Please enter a valid phone number']
    }
});
```

- **Middleware Hooks**:
    - Mongoose middleware allows you to define pre-save and post-save hooks to execute logic before or after saving data.
    - Example:

```javascript
userSchema.pre('save', function (next) {
    // Perform validation logic before saving
    if (!this.isAdmin) {
        // Do something
    }
    next(); // Call next to continue saving process
});
```

- **Error Handling**: 
    - Handle validation errors using Mongoose's error handling mechanism, which can be caught in promises or used with async/await syntax.
    - Example:

```javascript
newUser.save()
    .then(user => console.log('User created:', user))
    .catch(err => {
        if (err.name === 'ValidationError') {
            // Handle validation error
        } else {
            // Handle other errors
        }
    });
```

---
Created: April 18, 2024
Last Modified: `= this.file.mtime`
