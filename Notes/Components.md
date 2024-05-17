---
tags:
  - note
  - programming
language: JavaScript
Framework: React
---
# Components
---

`````ad-abstract
title: Components are UI Building Blocks
icon: code

Components are the *one* concept every React app, no matter its complexity, will use. They are the reusable building blocks that combine together to build the overall user interface. These components let you combine your markup, CSS, and JavaScript into one reusable line of code. A `<TableOfContents />` component could contain HTML code for the `<article>`, `<ol>` and `<li>` tags, along with custom CSS styling. 

![[Pasted image 20240201102626.png | center ]]

<br>

Each section of a website can be condensed into a single **component** that contains the code required to define the object.

For example, an image, title, and description is all that's required to make a `Core Concept` below, and each core concept can be exported to the next component to store all the Core Concept items.

![[Pasted image 20240201110006.png | center]]

<br>

```ad-caution
title: Component Functions Must Follow 2 Rules

- 1. Name starts with an ***<u>U</u>***ppercase Character
		- PacscalCase is the industry standard
- 2. Returns "Renderable" Content
		- In most cases: `Return` -> `JSX`
		- Also Allowed: `string`, `number`, `boolean`, `null`, `array` of allowed values

```

<br>

````ad-question
title: How can React tell the difference between custom and built-in components?
collapse:

All built-in elements like div, image, or header start with lowercase characters. Custom components on the other hand, so components built by you or other developers, must start with an uppercase character to tell React that it's not a built-in component.

```jsx
function App() {
  return (
    <div>
      <DisplayHeader />
      <main>
        <h2>Time to get started!</h2>
      </main>
    </div>
  );
}
```
````

<br>

## Why Components?

![[Pasted image 20240201110741.png | center]]
`````

---
Created: February 10, 2024
Last Modified: `= this.file.mtime`
