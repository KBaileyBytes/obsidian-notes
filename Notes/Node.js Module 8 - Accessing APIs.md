---
tags:
  - module
lecture_count: "7"
current_lecture: "7"
length: 1hr 22min
status: Complete
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13729056#learning-tools
module_number: 8
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [ ] Create API Endpoints
- [ ] Access them

```

``````ad-question
title: Q: How do we connect the front-end with the back-end?

Right now, we have these two distinct applications.

1. Back-end: We know how to take an address and convert that into a forecast.

2. Front-end: We know how to get our web application up and running in the browser with Express.

The real question is how do we integrate these two together?

What we need is for the browser to be able to communicate with the server, passing an address along. Then the server needs to convert that address into a forecast and pass it back to the browser, so the browser can actually render forecast data to the screen.

`````ad-check
title: A:
collapse:

HTTP JSON endpoints with Express.
`````

``````

``````ad-question
title: What are query strings and how do we use them?
collapse: 

### What are Query Strings?

A query string is a part of a URL that contains data to be passed to the server. It comes after the question mark `?` in a URL and consists of key-value pairs separated by ampersands `&`. Query strings are commonly used to send data from a client (e.g., a web browser) to a server in the form of parameters.

### Anatomy of a Query String:

```
?key1=value1&key2=value2&key3=value3...
```

Each key-value pair consists of a parameter name (key) and its corresponding value. Multiple key-value pairs are separated by ampersands.

### Example:

Consider a URL like this:

```
https://example.com/search?query=nodejs&category=tutorials&page=1
```

In this URL:

- `https://example.com/search` is the base URL.
- `?` denotes the beginning of the query string.
- `query=nodejs`, `category=tutorials`, and `page=1` are key-value pairs.

### How to Access Query String Parameters in Express.js:

In Express.js, you can access the query string parameters using the `req.query` object. Here's an example:

```js
const express = require('express');
const app = express();

app.get('/search', (req, res) => {
  const query = req.query.query;
  const category = req.query.category;
  const page = req.query.page;
  
  // Now you can use these parameters as needed
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

In this example, when a client makes a GET request to `/search?query=nodejs&category=tutorials&page=1`, Express.js parses the query string and makes the parameters available in the `req.query` object.



``````

``````ad-abstract
title: Accessing URL Parameters Example

URL:

```
http://localhost:3000/products?search=games&rating=5
```

<br>

Server:

````ad-code
title: app.js

```js
app.get("/products", (req, res) => {
  console.log(req.query);
  res.send({
    products: [],
  });
});
```
````

<br>

Response:

```js
{ search: 'games', rating: '5' }
```

<br>


`````ad-caution
title: Caution: You can only respond to a request ONCE

Otherwise you will get the following error:

```
Error [ERR_HTTP_HEADERS_SENT]: Cannot set headers after they are sent to the client
```

<br>

A common solution is returning the response like so:

````ad-code
title: app.js

```js
app.get("/products", (req, res) => {
  if (!req.query.search) {
    return res.send({
      error: "You must provide a search term.",
    });
  }

  res.send({
    products: [],
  });
});
```
````




`````


``````


## Building a JSON HTTP Endpoint

Making a JSON endpoint is straightforward. You just need to send a JS object back to the user. Ensure that de-structured parameters are given default values incase of `undefined`. 

````ad-code
title: app.js/weather

```js
app.get("/weather", (req, res) => {
  if (!req.query.address) {
    return res.send({
      error: "You must provide an address.",
    });
  }

  geocode(req.query.address, (err, { lat, long, location } = {}) => {
    if (err) {
      return res.send({
        err,
      });
    }

    forecast(lat, long, (err, forecast) => {
      if (err) {
        return res.send({
          err,
        });
      }

      res.send({
        forecast,
        location,
        address: req.query.address,
      });
    });
  });
});
```
````

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
