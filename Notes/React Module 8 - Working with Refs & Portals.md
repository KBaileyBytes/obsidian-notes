---
tags:
  - module
lecture_count: "22"
current_lecture: "22"
length: 1hr 24min
status: Complete
course_link: "[[React]]"
link: https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/39836236#overview
module_number: 8
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [ ] [[#Introduction to Refs]]
- [ ] [[#Intro to Portals]]
- [ ] [[#Ref API Functions]]

```


## Introduction to Refs

`useRef` is a Hook provided by React that allows you to create a mutable reference to a DOM element or a value that persists across renders. Unlike `useState`, updating the value returned by `useRef` does not trigger a re-render of the component.

This is a very simple hook that acts essentially as a variable for a single DOM element. With each element, you can give a `ref` property pointing to a `useRef()` variable. Accessing that variable gives you all of the DOM's current properties and values.

Here is an example converting a `useState()` to a `useRef()`:

````ad-code
title: Before.jsx

```jsx
import { useState } from "react";

export default function Player() {
  const [userInput, setUserInput] = useState("");
  const [playerName, setPlayerName] = useState();

  function handleNameChange() {
    setPlayerName(userInput);
    setUserInput("");
  }

  return (
    <section id="player">
      <h2>Welcome {playerName || "unknown entity"}</h2>
      <p>
        <input
          type="text"
          value={userInput}
          onChange={(e) => setUserInput(e.target.value)}
        />
        <button onClick={handleNameChange}>Set Name</button>
      </p>
    </section>
  );
}
```
````

````ad-code
title: After.jsx

```jsx
import { useState, useRef } from "react";

export default function Player() {
  const [userInput, setUserInput] = useState("");
  const playerName = useRef();

  return (
    <section id="player">
      <h2>Welcome {userInput || "unknown entity"}</h2>
      <p>
        <input ref={playerName} type="text" />
        <button onClick={() => setUserInput(playerName.current.value)}>
          Set Name
        </button>
      </p>
    </section>
  );
}
```
````

Also notice now we do not need to listen to the `onChange` event for the input, the Ref is already updating the value for us without re-rendering the page. This also seems useful for conditional styling purposes. 

`useRef` is a versatile Hook in React that allows you to create mutable references to DOM elements, store mutable values across renders, and cache values between renders without causing re-renders. It's commonly used for accessing and manipulating DOM elements, managing side effects, and optimizing performance.

````ad-code
title: Example.jsx
collapse:

```jsx
import { useRef } from 'react';

function App() {
    const input = useRef();
    
  return (
    <div id="app">
      <p>Please select an image</p>
      <p>
        <input data-testid="file-picker" type="file" accept="image/*" ref={input} />
        <button onClick={() => input.current.click()}>Pick Image</button>
      </p>
    </div>
  );
}

export default App;

```
````


### Using Refs Outside of DOM Element

You can further use `useRef` as a form of variable by giving a default value `useRef(0)` and accessing and manipulating it through the `current` property.

````ad-code
title: TimerChallenge.jsx

```jsx
import { useState, useRef } from "react";

export default function TimerChallenge({ title, targetTime }) {
  const timer = useRef();
  const [timerStarted, setTimerStarted] = useState(false);
  const [lostGame, setLostGame] = useState(false);

  function handleStart() {
    timer.current = setTimeout(() => {
      setLostGame(true);
      setTimerStarted(false);
    }, targetTime * 1000);
    setTimerStarted(true);
  }

  function handleStop() {
    clearTimeout(timer.current);
  }

  return ( ... );
}
```
````

If you have cases like this where you have a value that doesn't impact the UI, at least not directly, and you still need to manage it such that it's not reset when the component is re-executed, then you might have a great use case for a ref.


## Forwarding Refs & Modal Dialog

``````ad-abstract
title: `forwardRef`

### What is `forwardRef`?

- `forwardRef` is a function provided by React that allows a component to pass a `ref` received from a parent component down to a child component.

<br>

### Why use `forwardRef`?

- Some components need to access the underlying DOM element or child component directly. However, when components are wrapped in higher-order components or other abstractions, accessing refs can become challenging.
- `forwardRef` simplifies this process by allowing components to forward the `ref` received by the parent component to a specific DOM element or child component within the child component.

<br>

### Usage


```jsx
import { forwardRef } from "react";

const ResultModal = forwardRef(({ result, targetTime }, ref) => {
  return (
    <dialog ref={ref} className="result-modal">
      <h2>You {result}</h2>
      <p>
        The target time was <strong>{targetTime} seconds.</strong>
      </p>
      <p>
        You stopped the timer with <strong>X seconds left.</strong>
      </p>
      <form method="dialog">
        <button>Close</button>
      </form>
    </dialog>
  );
});

export default ResultModal;
```

`forwardRef` takes in one argument: the child component. Within that child you can still access or destructure props, but additionally `forwardRef` gives the child an additional parameter being the `ref` passed by the parent. This allows both the parent and the child to have access to that specific `useRef`.



``````


``````ad-abstract
title: The `<dialog>` tag

The **`<dialog>`** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element represents a modal or non-modal dialog box or other interactive component, such as a dismissible alert, inspector, or subwindow.

The HTML `<dialog>` element is used to create both modal and non-modal dialog boxes. Modal dialog boxes interrupt interaction with the rest of the page being inert, while non-modal dialog boxes allow interaction with the rest of the page.

JavaScript should be used to display the `<dialog>` element. Use the [`.showModal()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLDialogElement/showModal ".showModal()") method to display a modal dialog and the [`.show()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLDialogElement/show ".show()") method to display a non-modal dialog. The dialog box can be closed using the [`.close()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLDialogElement/close ".close()") method or using the [`dialog`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form#method) method when submitting a `<form>` that is nested within the `<dialog>` element. Modal dialogs can also be closed by pressing the Esc key.

````ad-code
title: Modal.jsx

```jsx
impot { forwardRef } from 'react';

const Modal = forwardRef((props, ref) => {
	return (
		<dialog ref={ref}>
			<p>The rest of the form ... </p>
			<form method="dialog">
				<button>Close</button>
			</form>
		</dialog>
	);
})
```
````

<br>

````ad-code
title: Parent.jsx

```jsx
import { useState, useRef } from "react";
import Modal from "./ResultModal";

export default function Parent(props) {
	const dialogRef = useRef();

	return (
		<>
			<Modal ref={dialogRef} />
			<button onClick={() => (dialogRef.current.showModal())}
		</>
	)
}
```
````



``````


`````ad-example
title: forwardRef API: `useImperativeHandle`

#### What is `useImperativeHandle`?

- useImperativeHandle is a React hook that allows a functional component to customize the instance value (the value that is exposed when using refs with `forwardRef`).

<br>

#### Why use `useImperativeHandle`?

- Sometimes, you want to expose certain functionality of a component to its parent component through a ref. However, you may want to customize what is exposed and how it's exposed.
- `useImperativeHandle` allows you to define which properties or methods of the component instance should be exposed via the ref, thus providing a cleaner and more controlled API to the parent component.
- This allows a clearer seperation of concerns, the component and each properties / methods that are exposed from it are all in one file.

<br>

#### Ex.

```jsx
import { forwardRef, useImperativeHandle, useRef } from 'react';

const ChildComponent = forwardRef((props, ref) => {
  const internalRef = useRef();

  useImperativeHandle(ref, () => ({
    methodName() {
      console.log('Method called from parent');
    },
  }));

  return <div>Component Content</div>;
});

export default ChildComponent;
```

<br>


```jsx
import React, { useRef } from 'react';
import ChildComponent from './MyComponent';

const ParentComponent = () => {
  const myRef = useRef();

  // Accessing exposed method
  myRef.current.methodName();

  return <ChildComponent ref={myRef} />;
};

export default ParentComponent;
```

<br>

#### Form example:

```jsx
import { forwardRef, useRef, useImperativeHandle } from 'react';

const Form = forwardRef((props, ref) => {
    const form = useRef();
    
    useImperativeHandle(ref, () => {
        return {
            clear() {
                form.current.reset();
            },
        };
    });
    
    return (
        <form ref={form}>
          <p>
            <label>Name</label>
            <input type="text" />
          </p>
    
          <p>
            <label>Email</label>
            <input type="email" />
          </p>
          <p id="actions">
            <button>Save</button>
          </p>
        </form>
    );
});

export default Form;
```




`````


``````ad-tip
title: setTimeout vs setInterval

````ad-code
title: setTimeout

```js
setTimeout(() => {
  console.log('Delayed function execution');
}, 1000); // Executes after 1 second

```
````

<br>

````ad-code
title: setInterval

```js
setInterval(() => {
  console.log('Repeated function execution');
}, 2000); // Executes every 2 seconds

```
````

<br>

### Differences:

1. **Execution**:
    
    - `setTimeout` executes the function once after the specified delay.
    - `setInterval` repeatedly executes the function at specified intervals until cleared.
2. **Control**:
    
    - `setTimeout` allows you to execute a function after a delay and does not repeat unless explicitly called again.
    - `setInterval` repeatedly executes the function at regular intervals until explicitly stopped using `clearInterval`.
3. **Use-Cases**:
    
    - Use `setTimeout` for one-time delayed tasks or animations.
    - Use `setInterval` for tasks that need to be performed repeatedly at regular intervals.
4. **Efficiency**:
    
    - Be cautious with `setInterval` as it may lead to performance issues if the interval is too short or if the callback function takes a long time to execute. Always consider the potential impact on performance when using `setInterval`.
5. **Clearing**:
    
    - Both `setTimeout` and `setInterval` return a unique identifier (an integer value), which can be used to clear or cancel the respective timer using `clearTimeout` or `clearInterval`.


``````


## Intro to Portals




---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
