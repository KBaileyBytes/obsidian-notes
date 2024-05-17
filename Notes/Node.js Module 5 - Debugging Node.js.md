---
tags:
  - module
lecture_count: "3"
current_lecture: "3"
length: 24min
status: Complete
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13728898#learning-tools
module_number: 5
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] [[#Debugging Node.js]]
- [x] [[#Reading Error Messages | Error Messages]]

```

## Debugging Node.js

``````ad-abstract
title:

The most basic debugging tool we have is something everyone has already used dozens of times before, `console.log`. It can be useful to quickly output variable contents, but sometimes you may want a more detailed look into your application.

In all cases that would be the Node Debugger. And that is Nodes' built in debugging tool which integrates with V8 and the Chrome browser. The debugger, like `console.log`, needs to be added at a specific point in your application. Node will pause the program at the specified point and allow you to view you application in that snapshot.

To start, add `debugger;` where you would like to pause the application.

```js
const addNote = (title, body) => {
  const notes = loadNotes();

  const duplicateNote = loadNotes().find((note) => note.title === title);

  debugger;

  // If there is not a duplicate note object
  if (!duplicateNote) {
    notes.push({
      title: title,
      body: body,
    });
    saveNotes(notes);
    console.log(chalk.green("New note added!"));
  } else {
    console.log(chalk.yellow("Ruh roh, duplicate!"));
  }
};
```


When we have debuggers in our application, they're not going to pause the program by default. We have to run Node with a special option to get that done. And to do this we use `node inspect` followed any additional arguments or commands needed.

![[Pasted image 20240211120340.png | center]]


The output we're seeing in the console is Node letting us know that a debugger is now up and running. We can see debugger, "Listening on," followed by this URL.

![[Pasted image 20240211130917.png | center]]


When started with the `--inspect` switch, a Node.js process listens for a debugging client. By default, it will listen at host and port 127.0.0.1:9229. Each process is also assigned a unique [UUID](https://tools.ietf.org/html/rfc4122).

Inspector clients must know and specify host address, port, and UUID to connect. A full URL will look something like `ws://127.0.0.1:9229/0f2c936f-b1cd-4ac9-aab3-f63b0f33d55e`.

Now you can use Chrome to inspect the application with: `chrome://inspect`. 

Under remote target, there are two targets. One at the port, and one at the shorthand local host. At the end of the day both are the exact same process, they're just duplicates. 

![[Pasted image 20240211131626.png | center]]


Now, from here we can actually inspect our application, and we can pause at that point in time we put the `debugger` statement and view all of our applications, variables, and values.

Let's get started by clicking `inspect` so we can actually open up a new instance of the debugger tools for debugging our node.js application.

![[Pasted image 20240211132252.png | center]]


Now it's important to note that at this point in time, not a single line of the program has executed. Right here, line one is highlighted, this is the line that the debugger is currently paused at. And when it's paused on a line, it hasn't executed that line yet. Meaning the variable has not yet been initialized.

On the right hand side, we have a lot of information about where our program currently is. So we have information about the call stack, we have the scope we currently have access to, and up above, we have tools for stepping through our application.

So currently the debugger is paused. To skip ahead to the `debugger` statement, we need to go ahead and manually tell Node to continue running the application by clicking the blue play button.

![[Pasted image 20240211133101.png | center]]


From here you have access to all variables and state of each object. In the call stack, we have some useful information about exactly where we are in the program. And under scope on the right side, we can actually see access to the variables we have in scope.

Now, we can always dive deeper into any of those values, by running some statements from the console.

For example, we could access body by typing it out. Or I could even grab something like one of the notes by referencing the notes array, and grabbing an item by index.

![[Pasted image 20240211133843.png | center]]

This way you can dump any object to the console, and make sure it's individual properties are what you're expecting.

<br>

Once finished with debugging, you can click the blue play button again which will run the program again until stopped or completion. If you want to run through the program again and debug it, you can enter `restart` in the Node terminal which will boot up another remote target.

![[Pasted image 20240211134344.png | center]]

``````

## Reading Error Messages

> Common sense...

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
