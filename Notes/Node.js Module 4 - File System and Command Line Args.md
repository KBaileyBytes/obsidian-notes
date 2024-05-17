---
tags:
  - module
lecture_count: "11"
current_lecture: "11"
length: 2hr 15min
status: Complete
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13728862#overview
module_number: 4
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [[#File System]]
- [[#Command Line Arguments]]
- [[yargs]]

```

## Command Line Arguments

````ad-abstract
title: 

When executing the `node` command, you can add additional arguments by chaining values with a space. Ex. `node app.js add --title="Title"`

These values that get added are put into the **`process.argv`** array:

```
[
  'C:\\Program Files\\nodejs\\node.exe',
  'C:\\Users\\Bromo\\Documents\\Programming\\Fullstack\\NodeJs\\node-course\\notes-app\\app.js',
  'add',
  '--title=Title'
]
```

````

## File System

````ad-abstract
title: Storing Data with JSON

The question we are aiming to answer here is what do we do with that data when our application gets it, we need to figure out how we can save it.
So if someone adds a note and then comes back tomorrow they can load that note up once again to read it or edit it.

Before this app, we'll be using the `FS` Core module to save all of our notes data to the file system.

Now what exactly is going inside of that file? Well, it's going to be [[JSON]] Data. In the example code below, we can read, parse, modify and save the contents of a JSON file.

```js
const bufferData = fs.readFileSync("./sandbox/1-json.json"); // Open
const dataJSON = bufferData.toString(); // bytes -> json (string, cant access properties)
const data = JSON.parse(dataJSON); // json -> JS Object
data.name = "Kyle Bailey";
data.age = 26;
const userJSON = JSON.stringify(data); // JS Object -> json
fs.writeFileSync("./sandbox/1-json.json", userJSON); // Save changes (also creates file if doesn't exist)
```

````

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
