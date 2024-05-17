---
tags:
  - module
lecture_count: "10"
current_lecture: "10"
length: 1hr 46min
status: Complete
course_link: "[[Node.js]]"
link: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/learn/lecture/13729078#learning-tools
module_number: 9
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] Git
- [x] GitHub
- [x] Heroku

```

## Git

```ad-tip
title: See Also

- [[Git Cheat Sheet]]
- 

```

````ad-abstract
title: What does `git init` actually do?

When you run the `git init` command, you're initializing a new Git repository in your current working directory. Here's what happens step by step:

1. **Creation of the `.git` directory**: Git creates a hidden directory named `.git` in your current working directory. This directory is where Git stores all the information and metadata related to version control for your project.
    
2. **Initialization of Git repository**: Within the `.git` directory, Git sets up the necessary files and directories to manage your repository. This includes the following:
    
    - `HEAD`: A pointer to the current branch or commit.
    - `config`: A configuration file containing settings for the repository.
    - `objects`: A directory where Git stores all the compressed data objects (blobs and trees) representing the files and directories in your project.
    - `refs`: A directory containing references to commits (branches and tags).
    - Other internal Git files and directories.

3. **No files are initially tracked**: At this point, Git is aware of the repository structure and configuration, but it hasn't started tracking any files yet.
    
4. **Potential creation of a new `.gitignore` file**: After running `git init`, you might want to create a `.gitignore` file to specify which files and directories Git should ignore (e.g., build artifacts, temporary files, dependencies). This file helps keep your repository clean and prevents unrelated files from being tracked.
	- When you're using npm, you should add the `/node_modules/` folder to the `.gitignore` file. This directory is generated with `npm install` and contains large amounts of external code unrelated to your project. This is the best industry practice.
````


## Heroku

```ad-tip
title: See Also

- [[Heroku CLI Cheat Sheet]]
```

``````ad-abstract
title: Setting up SSH Keys

In order to connect Git and Heroku, we need to authenticate the connection with [[SSH]] keys. These keys are frequently managed by an [[SSH Agent]] for the developers convenience.

Run the command `eval $(ssh-agent -s)` to start the SSH agent up. This essentially prepares your system to securely manage your SSH keys. This command is typically run once per session or per shell instance to start the SSH agent and set up necessary environment variables. This ensures your SSH keys are available for authentication when needed.

`````ad-tip
title: Destructuring `eval $(ssh-agent -s)`
collapse:

1. `ssh-agent -s`: This command starts the SSH agent in the background and prints out the necessary commands to set up the environment variables. The `-s` option is used to generate Bourne shell-compatible output.
    
2. `$(...)`: This is command substitution in the shell. Whatever is inside the `$(...)` is executed first, and its output is used as part of the outer command.
    
3. `eval`: This command evaluates the result of the command substitution as if it were entered directly into the shell. It's commonly used to set environment variables dynamically.

4. Output: When running correctly, the command will output something like the following:
	- `Agent pid 1234`
	- `Agent` refers to the SSH agent process that has been started.
	- `pid 1234` is the process ID. It's a unique identifier assigned to the SSH agent process by the operating system. This ID can be used to interact or terminate the SSH agent process if needed. 
`````

Next, you need to add your private SSH key to the SSH agent: `ssh-add ~/.ssh/id_rsa`



``````

````ad-example
title: Deploying to Heroku

### 1. Creating the Heroku Application

After connecting your SSH keys, you can freely create applications using the `heroku create {name}` command. The name must be unique accross *all* Heroku applications.

This will output 2 urls:

1. The live URL
2. The GIT repository *for* the live URL

This will reserve the space and push your code to the Heroku servers. Note that at this time, the application is **not** deployed.

<br>

### 2. Modify `package.json` for Deployment

Before deploying, we musy ensure that our program is ready to be deployed, and that Heroku will know how to run the application. To do that, we have to modify the `package.json` file so that Heroku can run the `node src/app.js` command. This can be added to the `scripts` object.

```json
{
  "name": "web-server",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node src/app.js",
    "dev": "nodemon src/app.js -e js,hbs"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.16.4",
    "hbs": "^4.0.1",
    "request": "^2.88.0"
  }
}
```

Note that the `scripts` object can be accessed through the node CLI to make life a little easier for developers. You can use the `npm run` command and giving the name of the specific script to run:

```
npm run start
```

<br>


### 3. Modify `app.listen()` for Heroku's Servers

Heroku provides us with a port value to listen to while your app is running. This will not be a static value and it's provided to the application through an environment variable set at the OS level. You can extract this variable from `process.env.PORT`. Since this variable will be undefined locally, it's frequently paired with the logical *OR* operator like so:

```js

// ...

const app = express();
const port = process.env.PORT || 3000;

// ...

app.listen(port, () => {
  console.log("Server is running on port " + port);
});
```

<br>

### 4. Modify Fetch Requests

If you have client side JS that gets data from a local fetch request, you have to modify the URL to match Heroku's server. AKA don't try and access `localhost` and just use the root shorthand like so:

```js
fetch(`/weather?address=${location}`).then((res) => {
    res.json().then((data) => {
      if (data.error) {
        console.log("Error: " + data.error);
        errorMessage.textContent = `Error: ${data.error}`;
        dataMessage.textContent = "";
      } else {
        console.log(`
      Location: ${data.location}
      Forecast: ${data.forecast}
      `);
        dataMessage.textContent = `
      ${data.location}
      ${data.forecast}
      `;
      }
    });
});
```

<br>

### 4. Push Updated Changes to Heroku + Deploy

To deploy your app, all you have to do is push the updated application to the remote that Heroku set up for us. 

```
git push heroku main
```

When Heroku sees that new commits have been pushed, it's going to deploy our application again. It will install the dependencies and initiate the server.

And that's it! Deployment complete. You should now be able to view your website and monitor it's statistics on Heroku.


````



---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
