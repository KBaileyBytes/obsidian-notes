---
tags:
  - module
lecture_count: "7"
current_lecture: "7"
length: 29min
status: Complete
course_link: "[[React]]"
link: https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/39836178#overview
module_number: 7
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] Common Errors
- [x] [[#Using Breakpoints & Debugger]]
- [x] [[#React Strict Mode & Why]]
- [ ] [[#React DevTools Extension]]

```

![[Pasted image 20240306121625.png | center | 700]]

Mostly common sense, first line is the main error message with the location of the error in the link below it. You can click the arrow to view the stack-trace which is a list of code executions that led to this error.

![[Pasted image 20240306121922.png | center | 700]]

A common way to avoid outputting data that doesn't exist is to make a "guard clause" or an early return. This way, the function returns a value and exits before attempting to calculate or output anything.

````ad-code
title: Results.jsx

```jsx
import { calculateInvestmentResults, formatter } from "../util/investment.js";

export default function Results({ input }) {
  const results = [];
  calculateInvestmentResults(input, results);

  if (results.length === 0) {
    return <p className="center">Invalid input data provided.</p>;
  }

  const initialInvestment =
    results[0].valueEndOfYear -
    results[0].interest -
    results[0].annualInvestment;

  return ( <p> ... </p> );
}
```
````


## Using Breakpoints & Debugger

Using the DevTools in the browser is fairly straightforward. For Firefox you can access the `Debugger` tab or for Chrome you can access the `Sources` tab.

| Firefox                                      | Chrome                                |
| -------------------------------------------- | ------------------------------------- |
| ![[Pasted image 20240307100919.png \| 600 ]] | ![[Pasted image 20240307100950.png ]] |

From here, you can access your directory structure and files and place breakpoints where needed by clicking on a line. Once the application stops at a breakpoint, you can now use the controls provided by the debugger to step by step walk through our code.

There are 4 common debugger commands:

1. **Resume**
	- Resumes application until next breakpoint or completion.
2. **Step Over**
	- The most common command; jumps to the next statement in the current function.
3. **Step In**
	- Jumps to the definition of the method that's about to be executed
4. **Step Out**
	- Steps out of the current function.

This allows us to walk through the code and see how it behaves and view variables and their contents.


## React Strict Mode & Why

````ad-abstract
title: What is Strict Mode?

React Strict Mode is a tool provided by React that helps developers catch potential problems in their applications during development. It is not primarily for debugging, but rather for *identifying and addressing common mistakes and potential issues early in the development process*.

When you wrap a portion of your React application in `<React.StrictMode>`, React enables a set of strict checks that are designed to highlight potential problems in your code.
````

A common use-case is wrapping your `<App />` component to enforce these rules on the whole application.

````ad-code
title: index.jsx

```jsx
import ReactDOM from "react-dom/client";
import { StrictMode } from "react";

import App from "./App.jsx";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```
````

---

One of the most important things the StrictMode component does during development is that it will execute every component function twice instead of just once.

## React DevTools Extension

This browser extension gives you some excellent utility as a React developer. It gives two extensions to your browser DevTools: **Profiler** and **Components**.

#todo - write notes on profiler

**Profiler** is primarily about finding and fixing performance issues in your application.

**Components** allows you to view all aspects of your application component tree. You can view props and their values directly from the devtools. If the component manages state you will also see that under `hooks`.



---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
