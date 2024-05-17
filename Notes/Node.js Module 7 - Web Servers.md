---
tags:
  - module
lecture_count: "11"
current_lecture: "11"
length: 2hr 22min
status: Complete
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13728970#learning-tools
module_number: 7
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [ ] [[#Using Express]]

```

## Using Express

```ad-abstract
title: See Also
- [[Express]]
```

---

``````ad-tip
title:

Express makes it really easy to create web servers with Node.

These servers are going to allow us to serve up assets for our web application. This includes HTML, CSS, client-side JavaScript, and JSON data.

<br>

---

<br>

![[Pasted image 20240228114009.png | center | 400]]

After initializing your project with `npm init -y` and having a similar directory structure to the reference above, you can `require` or `import` the library. What the Express Library exposes is just a single function.

So Express is actually a function, as opposed to something like an object and we call it to create a new Express application.

````ad-code
title: app.js

```js
const express = require("express");

const app = express();
```
````

<br>

The Express function doesn't take in any arguments. Instead, we configure our server by using various methods provided on the application itself.

That means our Express application is above is ready to be told what exactly it should do below.


<br>

---

<br>

```js
// app.com
// app.com/help
// app.com/about
```

So, above we have one domain, app.com and all of it's gonna run on a single Express server.

What we have set up though are multiple routes. We have the `root route`, we have, `/help`, we have, `/about` and we could add others.

We set that up using a method on app called `get()`. This lets us configure what the server should do when someone tries to get the resource at a specific URL.

<br>

So in this case, when someone visits the homepage (represented by "") this function would describe what to send back to them.

```js
// app.com

app.get("", (req, res) => {

  res.send("Hello express");

});
```

The second argument, is a function that gets called with two very important arguments. 

The first is an object containing information about the incoming request to the server. This is commonly called **req**, which is short for request. You'll see this used throughout the documentation. The other argument is the response. This contains methods allowing us to customize what we're gonna send back to the requester. This is commonly called **res**, which is short for response.

Within the function, you can analyze the request object to decide how to proceed. Ex. HTML, database call, JSON etc..

<br>

#### Displaying Text

From here we can easily display some text in the browser. To get that done you can use `res.send()`.

This allows us to send something back to the requester. So if someone's making a request from code, using something like the NPM request library, they'll get what you give as a parameter.

```js
res.send("Hello express!");
```

If they're making the request from the browser, this is what's going to display in the browser window.

<br>

The last step is to start the server up. We have to use one more method on `app` which will only ever use a single time in our application, that is, `app.listen()`.

This starts up the server, and it has it listen on a specific port given by the first parameter in the method.

A common development port is port 3000, but it is obiously not the default port. When you visit a website you don't provide the port because there are default ports. For example, for an HTTP based website it is port 80.

The other optional argument we can pass to the listen method is a callback function which just runs when the server is up and running.

The process of starting up a server is a asynchronous process though it'll happen almost instantly.

A common practice is to print a message to the console just letting the person who's running the application know the server did start correctly.

```js
app.listen(3000, () => {
	console.log("Server is running on port 3000.");
})
```

<br>

After booting up the server with `node src/app.js`, let's go ahead and visit it in the browser.

Since we're running the server on our local machine, we're not gonna be able to access it off of our machine, and we're not gonna be able to access it from a real domain. We'll learn how to do that sort of thing when we explore production deployment.

For now, the server is only accessible on our machine and we can access it at `localhost`. Now it's localhost port 3000, which is represented in the URL as `localhost:3000`. It's 3000 because that is the port we chose to listen on when we called, `app.listen()` with it's first argument.


<br>

### Serving HTML and JSON

When sending data back to the user, we're either going to send back HTML designed to be rendered in the browser, or we're going to send back JSON designed to be consumed and used by code. To achieve this, we just change what we pass inside `res.send()` to fit our needs.

````ad-code
title: app.js

```js
const express = require("express");

const app = express();

// app.com
app.get("", (req, res) => {
  res.send("<h1>Weather</h1>");
});

// app.com/help
app.get("/help", (req, res) => {
  // res.send({
  //   name: "Kyle",
  //   age: 26,
  // });

  res.send([{ name: "Kyle" }, { name: "Sara" }]);
});

// app.com/about
app.get("/about", (req, res) => {
  res.send("<h1>About page</h1>");
});

// app.com/weather
app.get("/weather", (req, res) => {
  res.send({ forecast: "50", location: "Winnipeg" });
});

app.listen(3000, () => {
  console.log("Server is running on port 3000.");
});
```
````

<br>

### Serving Static Assets


````ad-attention
title: Node.js Global Variables

In Node.js, `__dirname` and `__filename` are special global variables that provide information about the current directory path (`__dirname`) and the current filename with the full path (`__filename`).

1. **`__dirname`**:
    
    - `__dirname` returns the directory name of the current module. It represents the absolute path to the directory containing the currently executing file.
    - This variable is particularly useful for tasks like resolving the path to other files relative to the current file, regardless of where the application is being run from.
2. **`__filename`**:
    
    - `__filename` returns the filename of the current module with the absolute path.
    - It provides the full path of the current module's file, including the file name itself.
    - This can be helpful when you need to know the exact location of the currently executing file, for tasks like logging or dynamically constructing paths relative to the current file.


Here is an example output from a `console.log()` call:

```
C:\Users\Bromo\Documents\Programming\Fullstack\NodeJs\node-course\web-server\src
C:\Users\Bromo\Documents\Programming\Fullstack\NodeJs\node-course\web-server\src\app.js
```

````
In the `app.js` file above, we can render some HTML for pages like the homepage and the about page.

Now Node.js applications can indeed send back HTML, but typing HTML in a string in a JavaScript file is going to get out of hand quickly as we add more to the given web page.

It would be nice if we could write our HTML in separate HTML files or an entire directory that could contain HTML files, CSS files client side JavaScript videos, images and more, and have the [[Express]] server serve those up.

A common approach would be to create a `public` directory to contain all the files that will be served up such as HTML files or JavaScript files. 

One important piece of information we need is the ***path*** to the public folder. It needs to be an absolute path from the root of your machine. We'll use the core Node module with the same name to get this.

```js
path.join(__dirname, "../public")
```
With the `join()` function, you can use the global directory variable along with regular console commands to tell Express which directory you want to serve. This case being the `public` directory.

![[Pasted image 20240302122137.png | center]]


<br>

## Serving Dynamic Assets

In the image above chose to put all of our static assets in the public directory.

Everything inside of there was made available via the web server. This included the CSS images, JavaScript and HTML documents that we wanted users in the browser to be able to access.

Now static means that they do not change. I could refresh the home page 500 times and I would always get the exact same result.

````ad-abstract
title: Setting Up a Template Engine


We'll use what's called a *template engine* to render dynamic webpages using Express. Now, the template engine that we'll set up is called **Handlebars**.


```ad-tip
title: Handlebars
collapse:

Handlebars allows us to do two very important things:

1. Render dynamic documents.

2. Easily create reusable code.

By googling NPM Handlebars we can see it is a very popular templating tool. It is a low level library that implements Handlebars in JavaScript. It can be used in a wide variety of settings like the browser, the server, desktop applications with Electron or anywhere else that JavaScript can be used.
```

For our purposes we want to use Handlebars with our Express server. The Handlebars module isn't going to let us get that done on it's own. There is another library though which is like a plugin for Express that essentially integrates Handlebars into Express called ***hbs***.

After installing through npm, setting up hbs is straightforward. We need to tell Express which templating engine we installed through the `set` method.

```js
app.set("view engine", "hbs");
```
`set` allows you to set a value for a given Express setting and there are a few. It takes two parameters; a key being the setting name and the second being a value which we want to set it to. The key is case sensitive.

````

When we're working with Express, it expects all of your views (in this case, our Handlebars templates) to live in a specific folder that is in the root of the project called `/views`.

Within that folder, you can create views to render. Such as `/views/index.hbs`. A Handlebars file is nothing more than HTML with a couple of nice to have features for injecting dynamic values such as `{{ }}` to access given values from the server.

````ad-code
title: index.hbs

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Express</title>
    <link rel="stylesheet" href="styles.css" />
    <script src="js/app.js"></script>
  </head>
  <body>
    <h1>{{title}}</h1>
    <p>Created by {{name}}</p>
  </body>
</html>
```
````

To actually serve up this template we need to set up a route on the server. So once again that'll be an `app.get(route, (req, res) => {})` call.

Since it's our index file we can leave the first string empty. Then as the second argument we'll have our function with `request` and `response` as the two arguments.

```js
app.get("", (req, res) => { });
```

Now inside of the function, the only way we've ever sent information back to the requester previously is via `response.send()`. We saw how we could send back a string or an HTML string or even an object or an array which would get converted to JSON.

In this case, the goal is to not use `send()` but to use `render()`. Render allows us to render one of our views. We've configured Express to use the view engine `HBS`. So with `render()`, we can render one of our Handlebars templates.

```js
app.get("", (req, res) => {
	res.render("index", { optional: data, name: "Kyle" });
})
```

The first argument is the name of the view to render and the second argument is an object which contains all of the values you want that view to be able to access. So by calling `res.render()`, Express retrieves that view, and converts it into HTML with all of the dynamic values in place.

````ad-question
title: How can you customize the location and name of the `/views` directory?
collapse:

With `/views` being the default directory name that Express uses, it's important to know how to customize it.

Within `app.js`, you need to set the `views` setting to the new name you've set the folder to.

```js
const viewsPath = path.join(__dirname, "../templates");

app.set("views", viewsPath);
```
````

<br>

### Creating Handlebar Templates

Partials, as the name suggests, allows you to create a small reusable template which is part of a larger webpage. That's where partial comes from.

So think about parts of the webpage that you're going to end up reusing across multiple pages in your site. This would be things like headers or footers where you want the exact same thing showing on every page to give your site a nice unified feel.

Before creating partials, first we need to configure `hbs` on the server side. First we should adjust our directory structure by seperating the partials and the views like so:

![[Pasted image 20240304192832.png | center]]

Then we can configure our `app.js` file appropriately. First we should import the `hbs` module. Once we have it the only thing that we need to do is tell Handlebars where we are going to put our partials like so:


```js
const hbs = require("hbs");

const partialsPath = path.join(__dirname, "../templates/partials");

hbs.registerPartials(partialsPath);
```

<br>

`````ad-info
title: How to render a partial

After configuring hbs within our app, we can create and use partials accross all views. We can continue using the `{{}}` syntax, but now to tell Handlebars that we want to render a partial, we can add `>{partial_name}` immediately after the opening bracket like so:

```html
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Express</title>
    <link rel="stylesheet" href="css/styles.css" />
    <script src="js/app.js"></script>
  </head>
  <body>
    {{>header}}
    <p>Created by {{name}}</p>
  </body>
</html>
```
`````


<br>

`````ad-warning
title: Nodemon gotcha!

If you're executing you're app with Nodemon, it's easy to forget that Nodemon will *not* trigger a refresh if a `.hbs` file is modified or added if you're using the default command.

You can easily address this by customizing the nodemon command to include `.hbs` files. This can be done by adding the `-e` flag after the path, and adding each extension you want to includ in a comma seperated list like so:

```
nodemon src/app.js -e js,hbs
```

`````

<br>

### 404 Pages

Adding a catch-all route at the end of your Express.js routes allows you to handle requests that don't match any of the defined routes. This is typically used to serve a 404 page, indicating that the requested resource was not found.

Whenever a request is made, Express will look through the application top down until it finds a route that matches the request. So you can use the wildcard character to match all routes like so:

````ad-code
title: app.js

```js
// All other requests

app.get("/help/*", (req, res) => {
  res.render("404", {
    message: "Help article not found.",
  });
});

// Catch all
app.get("*", (req, res) => {
  res.send("My 404 page");
});

// ...
```
````


``````


---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
