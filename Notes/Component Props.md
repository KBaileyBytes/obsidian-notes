---
tags:
  - note
  - programming
  - react
language: JavaScript
Framework: React
---
## Configuring Components with Props

`````ad-abstract
title:

Just as you can build and reuse JavaScript functions with different data, we also might want to build and reuse certain React Components with different input data. And that's why React offers another crucial concept that's related to components called <u>*props*</u>.

React components use props to communicate with each other. Every parent component can pass data to its child components by giving them props. Props might remind you of HTML attributes, but you can pass any JavaScript value through them, including objects, arrays, and functions and they get grouped together into a single object usually called `props`.

![[Pasted image 20240204100006.png | center]]

<br>

```jsx
function CoreConcept(props) {
  return (
    <li>
      <img src={props.image} alt={props.title} />
      <h3>{props.title}</h3>
      <p>{props.description}</p>
    </li>
  );
}

function App() {
  return (
    <div>
      <DisplayHeader />
      <main>
        <section id="core-concepts">
          <h2>Core Concepts</h2>
          <ul>
            <CoreConcept // Each value gets put into the props object
              title="Components"
              description="The core UI building block."
              image={componentsImg}
            />
            <CoreConcept />
            <CoreConcept />
            <CoreConcept />
          </ul>
        </section>
      </main>
    </div>
  );
}
```
<br>

### Destructuring Props

You can also use another JavaScript feature within the parameter list called **destructuring**. You can use object destructuringby adding opening and closing curly braces within the parameter brackets. These opening and closing curly braces are used to destructure the first parameter of this function, so the <u>props</u> parameter in this case. And object destructuring in JavaScript simply means that we can target the different properties of the incoming object by name.

```jsx

function CoreConcept({ image, title, description }) {
  return (
    <li>
      <img src={image} alt={title} />
      <h3>{title}</h3>
      <p>{description}</p>
    </li>
  );
}

// Or

function CoreConcept({ concept }) {
  return (
    <li>
      <img src={concept.image} alt={concept.title} />
      <h3>{concept.title}</h3>
      <p>{concept.description}</p>
    </li>
  );
}

```

<br>

### Using the Spread Operator


```js
// data.js (exclusing imports)
// not export default, has to be imported with:
// import { CORE_CONCEPTS } from "./data";
export const CORE_CONCEPTS = [
  {
    image: componentsImg,
    title: "Components",
    description:
      "The core UI building block - compose the user interface by combining multiple components.",
  },
  {
    image: jsxImg,
    title: "JSX",
    description:
      "Return (potentially dynamic) HTML(ish) code to define the actual markup that will be rendered.",
  },
  {
    image: propsImg,
    title: "Props",
    description:
      "Make components configurable (and therefore reusable) by passing input data to them.",
  },
  {
    image: stateImg,
    title: "State",
    description:
      "React-managed data which, when changed, causes the component to re-render & the UI to update.",
  },
];


```

<br>

Since in this case we'll be using each property and each property name, we can spread the data within the JSX parameter to extract each property without needing multiple lines of code.

<br>

```jsx
  <main>
	<section id="core-concepts">
	  <h2>Core Concepts</h2>
	  <ul>
		{CORE_CONCEPTS.map((concept, i) => (
		  // adding each property from the concept variable
		  // and adding another property for the key
		  <CoreConcept {...concept} key={i} />  
		))}
	  </ul>
	</section>
  </main>
```

<br>

### Default Prop Values


Sometimes, you'll build components that may receive and optional prop. For example, a custom `Button` component may receive a `type` prop.

So the button Component should be usable either with a type being set or without it.

<br>


```jsx

<Button type="submit" caption="My Button" />

// Or

<Button caption="My Button" />

```

<br>

To make this component work, you might want to set a default value for the `type` prop. This can easily be achieved since JavaScript supports *default values* when using object destructuring:


```jsx

export default function Button({ caption, type = "submit" }) { /* type has a default value of "submit" */ }

```

<br>

### The `children` Prop

Even if you're not setting any attributes, React will still give you a props object. It will just be an object with a handful of properties, but actually not entirely empty. Instead there is one prop which you will always get, the special, built-in `children` prop.

This is a prop that's set by React and it's a prop that's not set with help of attributes. The children prop here simply refers to the content between your component text. This way of building Components where your Components can wrap other Components or other content is called **Component Composition**.

Simplified, adding `props.children` to your component makes it a container of sorts, and allows React to know where you would like to display the `children` properties.

![[Pasted image 20240205120850.png | center]]


<br>

```jsx
export default function TabButton(props) {
  return (
    <li>
      <button>{props.children}</button>
    </li>
  );
}

// or

export default function TabButton({ children }) {
  return (
    <li>
      <button>{children}</button>
    </li>
  );
}
```
`````

---
Created: February 10, 2024
Last Modified: `= this.file.mtime`
