---
tags:
  - course
  - programming
course_name: The Complete Node.js Developer Course (3rd Edition)
instructor:
  - "[[Andrew Mead]]"
  - "[[Rob Percival]]"
category: Backend
language: JavaScript
documentation: https://nodejs.org/docs/latest/api/
link_to: https://www.udemy.com/course/the-complete-nodejs-developer-course-2/
current_lecture: "93"
total_hours: 35
sections: 18
lectures: 177
status: Ongoing
textbook:
  - "[[PDF-Guide-Node-Andrew-Mead-v3.pdf]]"
---
# `= this.file.name`
---

```bash
/Users/Bromo/mongodb/bin/mongod.exe --dbpath=/Users/Bromo/mongodb-data
```

**`= round(number(this.current_lecture) / number(this.lectures) * 100, 2)`% Lectures Complete!**
`= "<progress class='progress' value='" + this.current_lecture + "' max= '" + this.lectures + "'></progress>"`

````ad-example
title: Curriculum
icon: book

```dataview
table choice(status = "Archived", "<span class='cm-formatting cm-formatting-hashtag cm-hashtag cm-hashtag-begin cm-meta cm-tag-tag'></span><span class='cm-hashtag cm-hashtag-end cm-meta cm-tag-tag'>Archived</span>",
choice(status = "Ongoing", "<span class='cm-formatting cm-formatting-hashtag cm-hashtag cm-hashtag-begin cm-meta cm-tag-tag'></span><span class='cm-hashtag cm-hashtag-end cm-meta cm-tag-tag' style='color:yellow !important;'>Ongoing</span>",
choice(status = "Complete", "<span class='cm-formatting cm-formatting-hashtag cm-hashtag cm-hashtag-begin cm-meta cm-tag-tag'></span><span class='cm-hashtag cm-hashtag-end cm-meta cm-tag-tag' style='color:green !important;'>Complete</span>", "other"))) as "Status",
"<progress max=" + lecture_count + " value=" + current_lecture + "> </progress> " as Progress
from [[#]]
sort status desc, number(file.name) asc
```

````
# /project-template

```less
project-root/
│
├── node_modules/            // Dependencies installed via npm
│
├── public/                  // Static files (client-side JavaScript, CSS, images, etc.)
│   ├── css/                 // CSS files
│   ├── js/                  // Client-side JavaScript files
│   └── img/                 // Image files
│
├── views/                   // Templates (e.g., EJS, Pug)
│
├── routes/                  // Route handlers
│   ├── index.js             // Main routes
│   └── api.js               // API routes
│
├── controllers/             // Controllers for handling business logic
│
├── models/                  // Data models (e.g., Mongoose models for MongoDB)
│
├── src/                     // Optional, contains source code and/or MVC folders
│   └── app.js               // Entry point of the application, aka server.js
│
├── middleware/              // Custom middleware functions
│
├── config/                  // Configuration files
│   ├── database.js          // Database configuration
│   └── env.js               // Environment variables
│
├── tests/                   // Unit or integration tests
│
├── .gitignore               // Specify files to be ignored by Git
├── package.json             // Project dependencies and scripts
└── README.md                // Project documentation
```

# express-app-template.js

```
```


---
Created: January 4, 2024
Last Modified: `= this.file.mtime`
