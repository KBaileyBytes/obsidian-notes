---
tags:
  - module
lecture_count: "6"
current_lecture: "6"
length: 1hr 14min
status: Complete
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13728836#overview
module_number: 3
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] Learn how to use the Module system in 3 different ways:
	- [x] 1 Import core Node modules
	- [x] 2 Third party modules written by other developers / global modules
	- [x] 3 Modules that I've made

```

```ad-warning
title: Cloning Repositories

When downloading or cloning repositories online, that `.zip` file will not contain the `/node-modules` folder containing all of the external code. To fix this, you can run `npm install`. This will check both the `package` and `package-lock` `.json` files and install everything that's needed.

```

`````ad-example
title: Importing Modules

## Core Modules 

With a given Node module, you can import the class either through a variable, or directly importing the method into the app. See the [Documentation](https://nodejs.org/docs/latest/api/) for reference.


```js
const fs = require("fs");

try {
	fs.appendFileSync('message.txt', 'data to append');
	console.log('The "data to append" was appended to the file!");
} catch (err) {
	/* Handled */
}

// or

import { appendFileSync } from 'node:fs';

try {
	appendFileSync('message.txt', 'data to append');
	console.log('The "data to append" was appended to the file!");
} catch (err) {
	/* Handled */
}

```

<br>

## Local Modules

To import a local module, we still use the `require` function, but now we'll be passing it a _relative path_ to the file we want to export. Within that file, we need to specify what gets exported with `module.exports = {function_name}`.

````ad-quote
title: app.js
icon: code

```js
const getNotes = require("./notes.js");

console.log(getNotes());
```
````

<br>

````ad-quote
title: notes.js
icon: code

```js
const getNotes = function() {

	return "Your notes...";

};

module.exports = getNotes;
```

````

<br>

## Third-Party Modules Using NPM

In order to use `npm` in our project, we need to initialize it in the command line using `npm init`. This creates a configuration file called `package.json` that we can use to manage all of our [[dependency | dependencies.]]

Once `npm` is initialized, we can install and import packages from the [npm website](https://www.npmjs.com/). 

Ex. 
- `npm i validator@10.8.0`
- `npm i chalk@2.4.1`

Packages can be accessed by importing with the `require` function and the package name. (Possibly updated to `import` by now)

```js
const validator = require("validator");
const getNotes = require("./notes.js");

console.log(validator.isURL("https:/mead.io"));
```


`````

```ad-info
title: Global NPM Packages

When we install a module globally, we do not load the module in directly to our source file, and instead, we get a new command we can access through the terminal.

`npm i nodemon@1.18.5 -g`

When this gets installed, it will *not* show up in the `package.json` or `package-lock.json` file because it's functionality is held within the command line for the *developer* to use.

```

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
