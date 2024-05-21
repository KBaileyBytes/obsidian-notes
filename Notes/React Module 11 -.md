---
tags:
  - module
lecture_count: "16"
current_lecture: "1"
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
- [ ] Effects & Dependencies
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
- **Array with Dependencies**: The effect runs whenever the specified dependencies change.

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
collapse: 

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




`````


---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
