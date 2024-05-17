---
tags:
  - note
  - programming
---
# JSON
---

````ad-abstract
title: What is JSON?
> JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate.


JSON works really well with objects and arrays in JavaScript.

An object can model something like a book or a user or a note which has various properties to describe it in detail. And if we have an array of those things, then we have an array of items like we would in any database.

<br>

---

<br>

Right here as an example, let's start with a book variable whose value will be a new object. Now there are plenty of properties you could use to model a book. We're gonna stick with just two. We'll have the title for the book, which will be a string and we'll have the author for the book as well.

```jsx
const book = {
  title: "Ego is the Enemy",
  author: "Ryan Holiday",
};
```

So now we have our data stored as a JavaScript object and <u>the goal is to convert this into *JSON*</u> which is nothing more than a string so we can do something with it like save it to the file system. 

The first method we're gonna look at is `JSON.stringify`. This is a JavaScript method that takes in an object or an array or any value for that matter and it returns the JSON representation.

```js
JSON.stringify(book);
```

<br>

`JSON.stringify` takes in the object and gives us a JSON string back. However, the opposite of JSON.stringify would be `JSON.parse`, which takes in the JSON string and gives us back the JavaScript object.

```jsx
const bufferData = fs.readFileSync("./sandbox/1-json.json"); // Open
const dataJSON = bufferData.toString(); // bytes -> json (string, cant access properties)
const data = JSON.parse(dataJSON); // json -> JS Object
data.name = "Kyle Bailey";
data.age = 26;
const userJSON = JSON.stringify(data); // JS Object -> json
fs.writeFileSync("./sandbox/1-json.json", userJSON); // Save changes, creates file if doesn't exist
```


````

---
Created: `= this.file.ctime`
Last Modified: `= this.file.mtime`
