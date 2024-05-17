---
tags:
  - module
lecture_count: "14"
current_lecture: "14"
length: 3hr 36min
status: Complete
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13728908#learning-tools
module_number: 6
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] [[#Asynchronous Basics]]
- [x] [[#Non-blocking]]
- [x] [[ES6 - Objects]]
- [x] [[#Making Requests Without a Library]]

```

## Asynchronous Basics

``````ad-abstract
title:

`````ad-quote
title: app.js
icon: code

```js
console.log("Starting");

setTimeout(() => {
  console.log("2 Second Timer");
}, 2000);

setTimeout(() => {
  console.log("0 Second Timer");
}, 0);

console.log("Stopping");
```
`````

If the code above doesn't make sense, review the documentation or the [lecture](https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13728912#learning-tools). Node's asynchronous nature is also what makes it ***non-blocking*** (duh).

``````

## Non-blocking

`````ad-tip
title:

````ad-code
title: add()

```js
const add = (numOne, numTwo, callback) => {
  setTimeout(() => {
    callback(numOne + numTwo);
  }, 2000);
};

add(1, 4, (sum) => {
  console.log(sum);
});
```
````

This code demonstrates a common pattern in Node.js for handling asynchronous operations using callback functions. Instead of returning a value directly, asynchronous operations accept a callback function that will be called once the operation is completed. This allows Node.js to perform non-blocking I/O operations efficiently.

`````

## Making Requests Without a Library

````ad-code
title: 6-raw-http.js

```js
const http = require("http");
const request = http.request(
  `http://api.weatherstack.com/current?access_key=b5e3712337d1e7e129a9a97101da7831&query=40,-75&units=f`,
  (res) => {
    let data = "";

    res.on("data", (chunk) => {
      data = data + chunk.toString();
    });

    res.on("end", () => {
      const body = JSON.parse(data);
      console.log(body);
    });
  }
);

request.on("error", (error) => {
  console.log(error);
});

request.end();
```

#todo research more on chunks + on method
````

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
