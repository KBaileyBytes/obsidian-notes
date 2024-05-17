---
tags:
  - note
  - programming
language: JavaScript
Framework: React
---
# Javascript Syntax Extension
---

```````ad-abstract
title:

````ad-quote
title: App.jsx
icon: code

```jsx
function App() {
  return (
    <div>
      <header>
        <img src="src/assets/react-core-concepts.png" alt="Stylized atom" />
        <h1>React Essentials</h1>
        <p>
          Fundamental React concepts you will need for almost any app you are
          going to build!
        </p>
      </header>
      <main>
        <h2>Time to get started!</h2>
      </main>
    </div>
  );
}

export default App;
```
````

<br>

If you're unfamiliar with JSX, this file contains code that may be a bit confusing if you take a closer look because it seems to contain HTML code *inside* of a JavaScript function. And it also got this strange extension `.jsx`.

Well, this file, as well as the index.jsx file, has this extension because it is <u>a JavaScript file that uses non-standard JavaScript syntax</u>.

To be precise, it uses a JavaScript syntax extension called JSX which conveniently simply stands for **<u>J</u>avaScript <u>S</u>yntax <u>Ex</u>tension**. This extension allows developers to describe and create HTML elements by writing HTML markup code inside of JavaScript files.

The code you write as a React developer is transformed behind the scenes by the development server before reaching the browser with code that does compile in the browser.

<br>

## Using Dynamic Values

Outputting dynamic values is one of the key features of React applications. This can be done by inserting JavaScript code directly into the return statement which can be done in JSX and React by using curly braces, a single pair of curly braces opening and closing `{}`.

These braces can be inserted at any point within the code, within the `<img />` `src` tag, within a paragraph, etc. It has only 1 rule: <u>the inserted code must return a value that can be rendered by React</u>.

<br>

---

<br>

In the example below, we're storing the keyword value in a variable. This is considered best practice over directly inserting the expression within the return statement.

```jsx
const reactDescriptions = ["Fundamental", "Crucial", "Core"];

function getRandomInt(max) {
  return Math.floor(Math.random() * (max + 1));
}

function DisplayHeader() {
  const keyword = reactDescriptions[getRandomInt(reactDescriptions.length - 1)];

  return (
    <header>
      <img src="src/assets/react-core-concepts.png" alt="Stylized atom" />
      <h1>React Essentials</h1>
      <p>
        {keyword} React concepts you will need for almost any app you are going
        to build!
      </p>
    </header>
  );
}
```


<br>


## Dynamic JSX

In almost every React application, you'll come across scenarios where you may need to loop through data or only display components based off of a condition. You can use the ternary operator `{condition} ? {true output} : {false output}` or through the shortcut `{condition} && {true output}`.

```jsx
<div id="tab-content">
	{!selectedTopic ? (
	  <p>Please select a topic.</p>
	) : (
	  <>
		<h3>{EXAMPLES[selectedTopic].title}</h3>
		<p>{EXAMPLES[selectedTopic].description}</p>
		<pre>
		  <code>{EXAMPLES[selectedTopic].code}</code>
		</pre>
	  </>
	)}
</div>

// or

<div id="tab-content">
	{!selectedTopic && <p>Please select a topic.</p>}
	{selectedTopic &&  
	  (<>
		<h3>{EXAMPLES[selectedTopic].title}</h3>
		<p>{EXAMPLES[selectedTopic].description}</p>
		<pre>
		  <code>{EXAMPLES[selectedTopic].code}</code>
		</pre>
	  </>
	)}
</div>

// or put the JSX in a variable

```

<br>

````ad-important
title: JSX is capable of rendering arrays of data
collapse:

```jsx
<section id="core-concepts">
  <h2>Core Concepts</h2>
  <ul>
	{CORE_CONCEPTS.map((concept, i) => (
	  <CoreConcept {...concept} key={i} />
	))}
  </ul>
</section>
```
````

<br>


## Adding Styles Dynamically

Most attributes, like id and so on, are the same in JSX and HTML. But for the class attribute, it's actually different.

In JSX, you need to use `className` prop if you want to add a class to a button.

```jsx
export default function TabButton({ children, onSelect, isSelected }) {
  return (
    <li>
      <button className={isSelected && "active"} onClick={onSelect}>
        {children}
      </button>
    </li>
  );
}
```

<br>

```jsx
<TabButton
  isSelected={selectedTopic === "components"}
  onSelect={() => handleClick("components")}
>
  Components
</TabButton>
```

<br>

``````ad-abstract
title: Single File, Single Component

It's not recommended to have them all in the same file because as your React project grows and as you add more and more Components, this single file would grow. And working on those Components and finding the different Components would get harder and harder the more Components you have in that file.

Therefore, you typically store different Components in different files. Having multiple Components in the same file is a very rare exception, which you typically only go for if two Components are closely related and really only work with each other.

Typically, a developer would create a separate `components` subfolder which you add in the `src` folder. 

![[Pasted image 20240205114358.png | center | 500]]

Technically, this is not required, but it's a common choice and very common pattern. Additionally, any CSS related to the component would be created in a seperate `css` file with the same name as the component. In that Components folder, you would create your component code files like so:

````ad-quote
title: DisplayHeader.jsx
icon: code

```jsx

import reactImage from "../../assets/react-core-concepts.png";
import "./DisplayHeader.css";

const reactDescriptions = ["Fundamental", "Crucial", "Core"];

function getRandomInt(max) {
  return Math.floor(Math.random() * (max + 1));
}

export default function DisplayHeader() {
  const keyword = reactDescriptions[getRandomInt(reactDescriptions.length - 1)];

  return (
    <header>
      <img src={reactImage} alt="Stylized atom" />
      <h1>React Essentials</h1>
      <p>
        {keyword} React concepts you will need for almost any app you are going
        to build!
      </p>
    </header>
  );
}

```
````

<br>

`````ad-caution
title: CSS Styling

````ad-quote
title: DisplayHeader.css
icon: code

```css
header {
  text-align: center;
  margin: 3rem 0;
}

header img {
  height: 5rem;
  width: 10rem;
  object-fit: cover;
}

header h1 {
  margin: 0;
  font-family: "Roboto Condensed", sans-serif;
  font-size: 5rem;
  background: linear-gradient(40deg, #ea00ff, #ea00ff, #03d5ff, #03d5ff);

  -webkit-text-fill-color: transparent;
  filter: drop-shadow(0 2px 8px rgba(0, 0, 0, 0.5));
}

header p {
  margin: 0;
  font-size: 1.25rem;
  color: #8964b0;
  font-family: "Roboto Condensed", sans-serif;
}
```
````

Even though we're only importing the `DisplayHeader.css` file into our `DisplayHeader.jsx` component, these styles here are not scoped and limited to this DisplayHeader Component, we would get those styles being applied to any `header` element on the page.
`````
``````


```````

---
Created: February 10, 2024
Last Modified: `= this.file.mtime`
