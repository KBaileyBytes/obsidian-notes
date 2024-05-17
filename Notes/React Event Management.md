---
tags:
  - note
  - programming
  - react
language: JavaScript
Framework: React
---
# React Event Management
---

``````ad-abstract
title:

In React, you add event listeners to elements by adding a special prop attribute to those elements. We'll be calling it a prop here as well, because in the end those built-in elements are also just components. The special prop you want to add here is the `onClick` prop.

You can also not just add these event props on a button, but really on *any* element. Now the value for this onClick prop here, or actually for any event prop, is a **function**. You want to point at the function that should be executed when that event occurs.

```jsx
export default function TabButton(props) {
  function handleClick() {
    console.log("Clicked!");
  }

  return (
    <li>
      <button onClick={handleClick}>{props.children}</button>
    </li>
  );
}
```

<br>

```ad-caution
title: Event Functions

When giving a function value to an event, it is important to note that it's looking for the function <u>reference</u>. You do *not* want to call the function by adding the opening and closing brackets like so: 

`<button onClick={handleClick()}>{props.children}</button>`

This would call the function when the component renders, instead of when the event is fired.

```

<br>

`````ad-info
title: Passing Functions as Values

Often times, you may want to handle the event outside of the component code. For these situations, you can pass functions as values through the component tree to the desired component.

To achieve this, what we can do is we can simply accept a prop within the custom component that in this case will be named `onSelect`.

````ad-quote
title: TabButton.jsx
icon: code

```jsx
export default function TabButton({ children, onSelect }) {
  return (
    <li>
      <button onClick={onSelect}>{children}</button>
    </li>
  );
}
```
````

<br>

````ad-quote
title: App.jsx
icon: code

```jsx
function App() {
  function handleSelect() {
    console.log("Selected!");
  }

  return (
    <div>
      <DisplayHeader />
      <main>
        <section id="core-concepts">
          <h2>Core Concepts</h2>
          <ul>
            {CORE_CONCEPTS.map((concept, i) => (
              <CoreConcept {...concept} key={i} />
            ))}
          </ul>
        </section>
        <section id="examples">
          <h2>Examples</h2>
          <menu>
            <TabButton onSelect={handleSelect}>Components</TabButton>
            <TabButton onSelect={handleSelect}>JSX</TabButton>
            <TabButton onSelect={handleSelect}>Props</TabButton>
            <TabButton onSelect={handleSelect}>State</TabButton>
          </menu>
        </section>
      </main>
    </div>
  );
}
```
````

`````

<br>

````ad-info
title: Passing Argumewnts to Event Functions

If you need your event handler to display dynamic data based on which component event was fired, you can achieve this through passing arguments through the event functions.

We can do this by, instead of pointing at handler function, we can pass an arrow function to onSelect. By writing an arrow function, the even handler is now being pointed at the anonymous function instead of the handler itself. So, this allows you to add parameters to the handler function without it executing when the page loads.

```jsx
function App() {
  function handleClick(selectedButton) {
    console.log(selectedButton);
  }

  return (
    <div>
      <DisplayHeader />
      <main>
        <section id="core-concepts">
          <h2>Core Concepts</h2>
          <ul>
            {CORE_CONCEPTS.map((concept, i) => (
              <CoreConcept {...concept} key={i} />
            ))}
          </ul>
        </section>
        <section id="examples">
          <h2>Examples</h2>
          <menu>
            <TabButton onSelect={() => handleClick("components")}>
              Components
            </TabButton>
            <TabButton onSelect={() => handleClick("jsx")}>JSX</TabButton>
            <TabButton onSelect={() => handleClick("props")}>Props</TabButton>
            <TabButton onSelect={() => handleClick("state")}>State</TabButton>
          </menu>
        </section>
      </main>
    </div>
  );
}

```

````



``````

---
Created: February 10, 2024
Last Modified: `= this.file.mtime`
