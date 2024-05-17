---
tags:
  - note
  - programming
  - react
language: JavaScript
Framework: React
---
# React State Management
---

``````ad-abstract
title:

When a React application is running, each component, unless otherwise stated, only execute **once**. This means that if you are trying to update information through a local variable for instance, this will not trigger React to execute the function again and the UI will still contain it's original content. Essentially, if the JSX hasn't changed, the UI will not update.

```ad-info
title: How React Checks If UI Updates Are Needed

![[Pasted image 20240207104147.png | center]]

```

<br>

This is where **State** comes into play.

React components has a built-in state object. The state object is where you store property values that belong to the component. When the state object changes, the component re-renders with the new content.

In order to use state, we need to add an import statement from the `react` library and extract the object like so:

```jsx
import { useState } from "react";
```

This is called a React Hook. All these functions that start with <u>use</u> in React are Hooks. The special thing about those React Hooks is that they're technically regular functions but they must only be called inside of React component functions or inside of other React Hooks. It's essentially a variable with an alternate way to update it's data.

React Hooks must be initialized inside of Component Functions and only on the <u>top level</u>.

![[Pasted image 20240208115627.png | center]]


<br>

When calling `useState`, the function will actually return an array value which you can use array destructuring to store these two elements in two separate constants. Standard naming convention is `const [describeVariable, setDescribeVariable] = useState("Default value");`.

The first element in this array which we get back from useState, will be the current data snapshot for its component execution cycle. So when the component function is executed first it will be the value within it's parameters that's stored in the first element.

So the first element will be the actual *data* we're managing. The second element's naming convention always starts with `set` because in this array we get back from `useState` will always be a *function*. A function provided by React that can be executed to update this state or stored value.

But in a addition to updating this stored value, calling this special function will also tell React that component function that the state is in must be executed again, meaning the UI will be updated with any new information.

![[Pasted image 20240208121232.png | center]]

<br>


React *batches* state updates

React does a lot of work behind the scenes to optimize performance. Normally, this optimization doesn't really phase us. Because the typical flow is:

1. A user performs some action (like clicking a button).
2. The state variable is updated.
3. React's <u>reconciliation</u> process is triggered.
4. This process realizes that there's now a diff between the virtual DOM and the actual DOM.
5. React updates the actual DOM to reflect the changes in the virtual DOM.

In the vast majority of circumstances this all happens so fast as to appear, to the naked eye, as instantaneous. But the good folks who built React also put in some safeguards to protect against those instances where a developer tries to fire off a rapid series of state updates. Specifically, React goes out of its way to ensure that all state updates that are triggered within a loop will not actually be rendered until the loop has finished running.

<br>

```ad-question
title: How can we use `const` if it's value is changing?
collapse:

We can use `const` because it will be recreated every time the component function executes or updates. Behind the scenes React will store and update the actual value which will then be passed on to the constant when the component function executes again.

```

<br>

````ad-question
title: Why does `console.log()`'ing state return the old value?
collapse:

**React state is asynchronous**

When you update a React state variable, the subsequent mutation occurs *asynchronously*. You can prove it out with an example like this:

```jsx
export const MyComponent = () => {
  const [counter, setCounter] = useState(0);

  const increment = () => {
    setCounter(counter + 1);
    console.log('counter', counter);
  }

  return <>
    <div>
      Counter = {counter}
    </div>
    <button onClick={increment}>
      Increment
    </button>
  </>
}
```

<br>

From a UX perspective, the example above works just fine. Every time you click `Increment`, the counter value updates. However, the `console.log()` output will always be one update *behind*. This happens because the update occurs asynchronously. And when the code hits the `console.log()`, the value has not yet been updated.


````

<br>

````ad-quote
title: App.jsx
icon: code
collapse:

```jsx
function App() {
  const [selectedTopic, setSelectedTopic] = useState("Please click a button.");

  function handleClick(selectedButton) {
    setSelectedTopic(selectedButton);
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
          {selectedTopic}
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
