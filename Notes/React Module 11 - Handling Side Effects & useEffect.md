---
tags:
  - module
lecture_count: "16"
current_lecture: "16"
length: 1hr 21min
status: Ongoing
course_link: "[[React]]"
link: https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/8231828#overview
module_number: 1
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] What is a Side Effect
- [x] useEffect Hook
- [x] Effects & Dependencies
- [ ] When **not** to use useEffect

```

# React Side Effects

In React, side effects are operations that affect something __outside__ the scope of the function being executed. They are different from pure functions because they interact with external systems (e.g., APIs, the DOM, browser storage) and can produce changes that *aren't* strictly related to rendering the UI.


## The `useEffect` Hook

The `useEffect` hook is the most common way to handle side effects in React functional components.

### Basic Usage

```jsx
useEffect(() => {   
	// Your side effect code here   
	 
	return () => {     
		// Cleanup code here   
	}; 
}, [dependencies]);
```
### Dependency Array

- **Empty Array (`[]`)**: The effect runs only once, after the initial render.
- **Array with Dependencies**: The effect runs whenever the specified dependencies change *after* the initial render

### Cleanup Function

- Used to clean up resources to avoid memory leaks or unwanted behaviors.
- Typically involves clearing timers, unsubscribing from services, or other cleanup tasks.

```jsx
useEffect(() => {   
	const handle = setInterval(() => {     
		console.log('Interval running');   
	}, 1000);    
	return () => clearInterval(handle); 
}, []);

```

```ad-question
title: Side Effect Best Practices
collapse:

1. **Keep Effects Focused**: Each effect should ideally have a *single* responsibility.
2. **Use Cleanup Functions**: Always clean up subscriptions, timers, or any other resources that require cleanup.
3. **Dependency Management**: Ensure that the dependency array accurately reflects all variables that the effect relies on.
4. **Avoid Excessive Dependencies**: Be mindful of including functions or objects in the dependency array; this can lead to unnecessary re-renders.
```

`````ad-abstract
title: Persisting Data with LocalStorage

`localStorage` is a web API that allows you to store data in the browser. The data persists even after the browser is closed and reopened, making it useful for saving user preferences, state, or any other information you want to retain across sessions.


````ad-important
title: Basic Operations
collapse: 

##### Setter

```js
localStorage.setItem('key', 'Stringvalue');
```

##### Getter

```js
const value = localStorage.getItem('key');
```

##### Remove

```js
localStorage.removeItem('key');
```

##### Clear

```js
localStorage.clear();
```
````

<br>

````ad-note
title: Linking localStorage to State

```jsx
import { useState, useEffect } from 'react';

function App() {
  const [value, setValue] = useState('');

  useEffect(() => {
    const storedValue = localStorage.getItem('myKey');
    if (storedValue) {
      setValue(storedValue);
    }
  }, []);

  useEffect(() => {
    localStorage.setItem('myKey', value);
  }, [value]);

  return (
    <input
      type="text"
      value={value}
      onChange={(e) => setValue(e.target.value)}
    />
  );
}
```
````


`````

`````ad-example
title: Alternative Exposition of Modal Properties



````ad-code
title: before.jsx

```jsx
import { forwardRef, useImperativeHandle, useRef } from 'react';
import { createPortal } from 'react-dom';

const Modal = forwardRef(function Modal({ children }, ref) {
  const dialog = useRef();

  useImperativeHandle(ref, () => {
    return {
      open: () => {
        dialog.current.showModal();
      },
      close: () => {
        dialog.current.close();
      },
    };
  });

  return createPortal(
    <dialog className="modal" ref={dialog}>
      {children}
    </dialog>,
    document.getElementById('modal')
  );
});

export default Modal;
```

````

<br>

````ad-code
title: after.jsx

```jsx
import { useRef, useEffect } from "react";
import { createPortal } from "react-dom";

export default function Modal({ open, children }) {
  const dialog = useRef();

  useEffect(() => {
    if (open) {
      dialog.current.showModal();
    } else {
      dialog.current.close();
    }
  }, [open]);

  return createPortal(
    <dialog className="modal" ref={dialog}>
      {children}
    </dialog>,
    document.getElementById("modal")
  );
}
```
````


`````

## What are Effect Dependencies?

Effect dependencies are the values that, when changed, will trigger the re-execution of an effect. These are specified as an array in the second argument of the `useEffect` function. The dependency array tells React when to re-run the effect by comparing the current values of the dependencies to their values from the last render.

#### Ex.
```jsx
import { useState, useEffect } from "react";

export default function ExampleComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // This code runs after every render
    document.title = `You clicked ${count} times`;

    // Cleanup function (optional)
    return () => {
      // Cleanup code runs before the next effect or component unmount
    };
  }, [count]); // Effect depends on `count`

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount((oldState) => oldState + 1)}>
        Click me
      </button>
    </div>
  );
}

```


`````ad-warning
title: Using Function Dependencies

```jsx
import { useEffect } from "react";

export default function DeleteConfirmation({ onConfirm, onCancel }) {
  useEffect(() => {
    console.log("Timer set");
    const timer = setTimeout(() => {
      onConfirm();
    }, 3000);

    return () => {
      console.log("Cleanup Timer");
      clearTimeout(timer);
    };
  }, [onConfirm]); // onConfirm cleanup function in parent component

  return (
    <div id="delete-confirmation">
      // ...
    </div>
  );
}
```

When you pass a function as a dependency to a useEffect hook, the behavior depends on whether the function is *stable* or not. In React, functions (like other objects) are compared by reference. Each render creates new function references unless they are memoized using useCallback or similar.

#### What Happens with Function Dependencies

1. Effect Setup: The useEffect runs after the initial render and sets up the effect (in this case, setting a timer).
2. Effect Cleanup: When the dependencies change (i.e., the `onConfirm` function reference changes, when the parent component re-renders), the cleanup function from the previous effect run is executed. This ensures any resources like timers, subscriptions, or event listeners set up by the effect are properly cleaned up.
3. Effect Re-run: The effect is then re-run with the new function reference in its dependency array.


<br>

#### Why This Matters

If `onConfirm` changes frequently (which can happen if it’s defined inline or passed down from a parent component that redefines it on each render), the effect will constantly clean up and re-set the timer, leading to potential performance issues and unexpected behavior.

<br>

````ad-tip
title: Solving with useCallback

### What is `useCallback`?

useCallback returns a memoized version of a callback function that only changes if one of the dependencies has changed. This is useful for passing stable references to child components that rely on reference equality to avoid unnecessary renders.

It is a simple way to add security to your function dependencies without worrying about additional renders.

#### Basic Syntax
```jsx
const memoizedCallback = useCallback(() => {
	// Function logic here
}, [dependencies])
```


<br>

#### Example
```jsx
import React, { useState, useCallback } from 'react';

function ChildComponent({ onClick }) {
  console.log('ChildComponent rendered');
  return <button onClick={onClick}>Click me</button>;
}

function ParentComponent() {
  const [count, setCount] = useState(0);

  // Without useCallback, this function is re-created on every render
  // Therefore, pointlessly re-rendering the child component
  const handleClick = useCallback(() => {
    console.log('Button clicked');
  }, []); // Empty dependency array means this function is created only once

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <ChildComponent onClick={handleClick} />
    </div>
  );
}

export default ParentComponent;
```
````
`````

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
