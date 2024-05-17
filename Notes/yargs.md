---
tags:
  - note
language: JavaScript
Framework: Node.js
npm_link: https://www.npmjs.com/package/yargs
---
# **yargs** 🏴‍☠️
---
````ad-info
title: What is yargs?

Yargs helps you build interactive command line tools, by parsing arguments and generating an elegant user interface.

It gives you:

- commands and (grouped) options (my-program.js serve --port=5000).
- a dynamically generated help menu based on your arguments:

```
mocha [spec..]

Run tests with Mocha

Commands
  mocha inspect [spec..]  Run tests with Mocha                         [default]
  mocha init <path>       create a client-side Mocha setup at <path>

Rules & Behavior
  --allow-uncaught           Allow uncaught errors to propagate        [boolean]
  --async-only, -A           Require all tests to use a callback (async) or
                             return a Promise                          [boolean]
```

- bash-completion shortcuts for commands and options.
- and tons more.


````

````ad-example
title: Command Line Arguments With `yargs`

As you can see from [[Node.js Module 4 - File System and Command Line Args#Command Line Arguments | this example ]], if we wanted to process any information from the command line, we would have to process and manipulate each string value that gets added to the `process.argv` array. Node doesn't provide any argument parsing. It's a very bare bones utility, allowing us to just access the raw argument string.

So solve this issue, we can use the `yargs` npm package to access the `process.argv` array and process it for us. After installing with `npm i yargs` you can import the `yargs` variable into your app. To add *properties* to a command, you can add another property to the `builder` object.

```js
const chalk = require("chalk");
const yargs = require("yargs");
const getNotes = require("./notes.js");

// Customize yargs version
yargs.version("1.1.0");

// Create add command
yargs.command({
  command: "add",
  describe: "Add a new note",
  builder: {
    title: {
      describe: "Note title",
      demandOption: true,
      type: "string",
    },
    body: {
      describe: "Note body",
      demandOption: true,
      type: "string",
    },
  },
  handler: function (argv) {
	console.log(argv);
    console.log("Title: " + argv.title);
    console.log("Body: " + argv.body);
  },
});

// Create remove command
yargs.command({
  command: "remove",
  describe: "Remove a note.",
  handler: function () {
    console.log("Removing the note!");
  },
});

// Create read command
yargs.command({
  command: "read",
  describe: "Read a note.",
  handler: function () {
    console.log("Reading a note!");
  },
});

// Create list command
yargs.command({
  command: "list",
  describe: "List your notes.",
  handler: function () {
    console.log("Listing all notes!");
  },
});

// console.log(process.argv);
// console.log(yargs.argv);
yargs.parse(); // runs the application
```

<br>

The `yargs` package provides a more useful object for us to use:

```
$ node app.js add --title="My title." --body="My body."
{ _: [ 'add' ], title: 'My title.', body: 'My body.', '$0': 'app.js' }
Title: My title.
Body: My body.
```


````




---
Created: January 30, 2024
Last Modified: `= this.file.mtime`
