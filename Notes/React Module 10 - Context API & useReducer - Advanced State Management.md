---
tags:
  - module
lecture_count: "15"
current_lecture: "15"
length: 1hr 15min
status: Complete
course_link: "[[React]]"
link: https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/8244656#overview
module_number: 10
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [x] Solving the problem: Prop Drilling
- [x] Component Composition
- [x] Context API
- [x] useReducer

```


``````ad-question
title: How do we prevent Prop-drilling?

#### How do we apply this tree component without the inconvenience of prop drilling?

![[Pasted image 20240513113338.png | center]]


<br>

#### Solution 1: Component Composition
---

Component Composition can be part of the solution for prop drilling, but is often considered a best-practice over an actual answer. Doing this frequently will clutter your Parent components and should be used sparingly. Using the graph above, we can see that we essentially remove the connection tree for updating the cart, since the App component can directly communicate with the Product component if the Shop is modified to a wrapper, removing the need for the update prop passed between them.



`````ad-code
title: Shop.jsx

#### Before

````jsx
import { DUMMY_PRODUCTS } from '../dummy-products.js';
import Product from './Product.jsx';

export default function Shop({ onAddItemToCart }) {
  return (
    <section id="shop">
      <h2>Elegant Clothing For Everyone</h2>

      <ul id="products">
        {DUMMY_PRODUCTS.map((product) => (
          <li key={product.id}>
            <Product {...product} onAddToCart={onAddItemToCart} />
          </li>
        ))}
      </ul>
    </section>
  );
}
````
<br>

---

<br>

#### After

```jsx
export default function Shop({ children }) {
  return (
    <section id="shop">
      <h2>Elegant Clothing For Everyone</h2>

      <ul id="products">{children}</ul>
    </section>
  );
}
```
`````

<br>


#### Solution 2: Context API
---

With Context, you can connect your React state to that context value which is provided to the entire application.

And therefore, you can get rid of the extra props, state and state-updating functions.

<br>

![[Pasted image 20240513134108.png | center]]

<br>

React's Context API provides a way to pass data through the component tree without having to pass props down manually at every level. It's particularly useful when dealing with data that needs to be accessed by many components at different levels of the tree.

```ad-warning
title: When a context value changes each component using that value re-renders
```

<br>

```ad-question
title: What are some of Context API's usecases?
collapse:

### Common Use Cases of React's Context API

1. **Theme Switching**: Context API is ideal for managing themes across a React application. Instead of passing down the theme props to every component, you can use Context to provide the theme to any component that needs it.
    
2. **User Authentication**: When building applications that require user authentication, Context can be used to provide authentication state and user information to all components that need it, such as navigation bars, profile sections, or protected routes.
    
3. **Language Localization**: Context can be employed to manage language localization across the application. Rather than passing the selected language as props to every component, you can use Context to provide language information to components that need it.
    
4. **Global State Management**: Context can serve as a lightweight alternative to state management libraries like Redux or MobX for managing global application state. It allows you to share state across components without the need for prop drilling.
```

``````

```ad-tip
title: Context API Workflow

### *Define > Provide > Consume*

<br>

### Reducing Prop Drilling with Context API

Prop drilling refers to the practice of passing props through multiple layers of components unnecessarily. It can clutter the code and make it harder to maintain. React's Context API helps reduce prop drilling by providing a way to pass data down the component tree without explicitly passing props through every intermediate component.

Here's the Context API workflow:

1. **Define Context**: First, define a context using React's `createContext` function. This creates a context object that components can subscribe to.
    
2. **Provide Context**: Wrap the top-level components that need access to the context with a `Context.Provider` component. This component accepts a `value` prop, which provides the data to be shared.
    
3. **Consume Context**: Components that need access to the context can consume it using the `useContext` hook *or* by using the `Consumer` component (not industry standard / recommended). This allows them to access the context data without explicitly passing props.
```

`````ad-abstract
title: useContext Example

### Define
---

When defining contexts, it is common practice to store them in `./src/store/xyz-context.jsx` for data and state context storage.

From the file you can export the value returned from `createContext()` and provide it with a [[createContext Default Value | default value]]

````ad-code
title: shopping-cart.jsx

```jsx
import { createContext } from "react";

// Any value can be default value
export const CartContext = createContext({
  items: [],
});
```
````

<br>

### Provide
---

From here, we can Provide the context to the parent component by doing the following:

1. Import the context
2. Create the `<Context.Provider>` component
3. Provide the value property with a default value

<br>

````ad-code
title: App.jsx

```jsx
return (
    <CartContext.Provider value={shoppingCart}>
      <Header
        cart={shoppingCart}
        onUpdateCartItemQuantity={handleUpdateCartItemQuantity}
      />
      <Shop>
        {DUMMY_PRODUCTS.map((product) => (
          <li key={product.id}>
            <Product {...product} onAddToCart={handleAddItemToCart} />
          </li>
        ))}
      </Shop>
    </CartContext.Provider>
  );
```
````
<br>

### Consume
---

In order to consume the context, we simply import the context that we created and `useContext`. The returned value from `useContext` contains all the context values in it's current state.

```jsx
import { useContext } from "react";
import { CartContext } from "../store/shopping-cart";

export default function Cart({ onUpdateItemQuantity }) {
  const cartContext = useContext(CartContext);

  // ...cartContext.cart userContext.name etc
}
```

<br>

````ad-tip
title: Consumer Component Example

```jsx
import { CartContext } from "../store/shopping-cart";

export default function Cart({ onUpdateItemQuantity }) {
  return (
    <CartContext.Consumer>
      {(cartContext) => {
        // ...
        
        return (
          // JSX ...
        );
      }}
    </CartContext.Consumer>
  );
}
```
````


`````

`````ad-seealso
title: Applying State to Context

When applying context, it acts as a container for any items given to it. So, a convenient way to provide data and functions to your components is by making the context value an object with each related property as a field.

```jsx
  const cartContext = {
    items: shoppingCart.items,
    addItemToCart: handleAddItemToCart,
    updateCart: handleUpdateCartItemQuantity,
  };

  return (
    <CartContext.Provider value={cartContext}>
      <Header />
      <Shop>
        {DUMMY_PRODUCTS.map((product) => (
          <li key={product.id}>
            <Product {...product} />
          </li>
        ))}
      </Shop>
    </CartContext.Provider>
  );
```
Here, we can easily access the cart values along with any associated updating functions without prop drilling.

`````


`````ad-seealso
title: Outsourcing Context & State -> Provider Component

A common workflow for React developers is extracting all the Context logic and data into the `./store/` context file, this way each context added to the application can seperate it's logic into another `Provider` component without cluttering the `App.jsx` file.

````ad-code
title: shopping-cart.jsx

```jsx
import { createContext, useState } from "react";
import { DUMMY_PRODUCTS } from "../dummy-products";

// Any value can be default value
export const CartContext = createContext({
  items: [],
  addItemToCart: () => {}, // default values here are for auto-completion
  updateCart: () => {},
});

// Managing and providing context data
export default function CartContextProvider({ children }) {
	// ...
  }

  function handleUpdateCartItemQuantity(productId, amount) {
    // ...
  }

  const cartContext = {
    items: shoppingCart.items,
    addItemToCart: handleAddItemToCart,
    updateCart: handleUpdateCartItemQuantity,
  };

  return (
    <CartContext.Provider value={cartContext}>{children}</CartContext.Provider>
  );
}

```

````



`````


``````ad-abstract
title: Alternative State with useReducer

````ad-question
title: What is a reducer?

Put simply, a Reducer is a React function that reduced one or more complex values to a simple value

```
[5, 10, 100] (Reduce) => 115
```

````

<br>

### Introduction to React's `useReducer` Hook

The `useReducer` hook is a powerful alternative to `useState` for managing complex state logic in React applications. It is inspired by Redux and allows you to manage state transitions in a predictable way by dispatching actions to a reducer function.

<br>

### Use Cases of React's `useReducer` Hook

1. **Managing Complex State**: `useReducer` is well-suited for managing complex state logic, especially when state transitions depend on multiple factors or when state updates involve complex data structures.
    
2. **Form State Management**: When building forms with dynamic inputs or complex validation logic, `useReducer` can help centralize form state management and simplify the handling of form submissions and validation errors.
    
3. **Global State Management**: Similar to Redux, `useReducer` can be used to manage global application state. It allows you to define a single reducer function that handles state updates for different parts of your application.
    
4. **State with Complex Dependencies**: If your component's state depends on other parts of the state or external factors, `useReducer` can provide a clean way to handle these dependencies and update the state accordingly.




#### Dispatching Actions & Editing State with useReducer
---


````ad-code
title: SimpleCounter.jsx

```jsx
import React from 'react';

function counterReducer(state, action) {
    const { type } = action;
    
    switch (type) {
        case 'INCREMENT':
            return {
                count: state.count + 1
            }
        case 'DECREMENT':
            return {
                count: state.count - 1
            }
        case 'RESET':
            return {
                count: 0
            }
        default:
            return state
    }
}

function App() {
  const [countState, countDispatch] = React.useReducer(counterReducer, {
      count: 0,
  });
    
  return (
    <div id="app">
      <h1>The (Final?) Counter</h1>
      <p id="actions">
        <button onClick={() => countDispatch({ type: "INCREMENT" })}>Increment</button>
        <button onClick={() => countDispatch({ type: "DECREMENT" })}>Decrement</button>
        <button onClick={() => countDispatch({ type: "RESET" })}>Reset</button>
      </p>
      <p id="counter">{countState.count}</p>
    </div>
  );
}

export default App;
```
````

``````


---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
