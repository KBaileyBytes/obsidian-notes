---
tags:
  - module
lecture_count: "41"
current_lecture: "41"
length: 3hr 16min
status: Complete
course_link: "[[React]]"
link: https://www.udemy.com/course/react-the-complete-guide-incl-redux/learn/lecture/39659738?components=add_to_cart%2Cavailable_coupons%2Cbase_purchase_section%2Cbuy_button%2Cbuy_for_team%2Ccacheable_buy_button%2Ccacheable_deal_badge%2Ccacheable_discount_expiration%2Ccacheable_price_text%2Ccacheable_purchase_text%2Ccurated_for_ufb_notice_context%2Ccurriculum_context%2Cdeal_badge%2Cdiscount_expiration%2Cgift_this_course%2Cincentives%2Cinstructor_links%2Clifetime_access_context%2Cmoney_back_guarantee%2Cprice_text%2Cpurchase_tabs_context%2Cpurchase%2Crecommendation%2Credeem_coupon%2Csidebar_container%2Cpurchase_body_container#overview
module_number: 4
---
# `= this.file.name`
---

```ad-hint
title: Learning Objectives
icon: bullseye

- [ ] [[#Behind the Scenes of JSX]]
- [ ] [[#Structuring Components and State]]
- [ ] [[#Advanced State Usage]]
- [ ] [[#Patterns & Best Practices]]

```

## Behind the Scenes of JSX

``````ad-abstract
title: 

As you learned, React has a build process that's running behind the scenes that transforms and potentially optimizes our code such that it does work in the browser.

But as a React developer, you should know that, in theory, you could also build React apps without using JSX, and therefore, if you needed to, without using such a build process. Though this is a process that is very rarely applied in practice.

You could replace the JSX code on the left, which you might return in a component, with the code on the right, which does not use JSX at all, but which instead only uses standard JavaScript features.

![[Pasted image 20240213111422.png | center]]

They both output the same elements, just with different approaches. You could go for a non-JSX approach if you want a project that requires no build process.

<br>

### Fragment Components

In most (or possibly all) programming languages, functions will return a single value. That value could be a number, an object with many properties, or an array of nested objects, and JSX is no different.

That's why we need one wrapping element so that technically we return one value. Then internally that value stores the child components or remaining DOM tree. A common parent component is `div`, but frequently you'll want a component that will not show up on the DOM. That's where *Fragments* come in.

React gives you an alternative which you can use as a wrapper if you do need a root component.To use them, we can import `Fragment` from React and that's simply a component built into React that you can use like so:

```jsx
import { useState, Fragment } from "react";

// Old React Syntax
return (
	<Fragment>
		<Header />
		<main>
		...
		</main>
	</Fragment>
);

```

For modern React projects actually give you an even shorter alternative. There you don't even need to import fragment. You may still see `<Fragment>` in old projects where this syntax is not available.

```jsx
// New Fragment React Syntax
return (
	<>
		<Header />
		<main>
		...
		</main>
	</>
);

```

<br>

### When Should you Split Components?

````ad-quote
title: App.jsx
icon: code
collapse:

```jsx
import { useState } from "react";
import { CORE_CONCEPTS } from "./data";
import DisplayHeader from "./components/Header/DisplayHeader";
import CoreConcept from "./components/CoreConcept";
import TabButton from "./components/TabButton";
import { EXAMPLES } from "./data";

function App() {
  const [selectedTopic, setSelectedTopic] = useState("");

  function handleClick(selectedButton) {
    setSelectedTopic(selectedButton);
  }

  return (
    <>
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
            <TabButton
              isSelected={selectedTopic === "components"}
              onSelect={() => handleClick("components")}
            >
              Components
            </TabButton>
            <TabButton
              isSelected={selectedTopic === "jsx"}
              onSelect={() => handleClick("jsx")}
            >
              JSX
            </TabButton>
            <TabButton
              isSelected={selectedTopic === "props"}
              onSelect={() => handleClick("props")}
            >
              Props
            </TabButton>
            <TabButton
              isSelected={selectedTopic === "state"}
              onSelect={() => handleClick("state")}
            >
              State
            </TabButton>
          </menu>
          <div id="tab-content">
            {!selectedTopic && <p>Please select a topic.</p>}
            {selectedTopic && (
              <>
                <h3>{EXAMPLES[selectedTopic].title}</h3>
                <p>{EXAMPLES[selectedTopic].description}</p>
                <pre>
                  <code>{EXAMPLES[selectedTopic].code}</code>
                </pre>
              </>
            )}
          </div>
        </section>
      </main>
    </>
  );
}

export default App;
```
````

When an application or component contains logic and state for large sections sections of your website, as seen above, you may run into some unexpected "bugs". When you manage state on such a large level, it's easy to forget that when state changes, React will re-render the ***component*** the state is in. So if you have your entire state and logic handled at the `App.jsx` level, the entire application will re-render with possibly new data.

To avoid this, break down components and seperate logic into different files.

````ad-quote
title: App.jsx
icon: code

```jsx
import DisplayHeader from "./components/Header/DisplayHeader";
import CoreConcepts from "./components/CoreConcepts";
import Examples from "./components/Examples";

function App() {
  return (
    <>
      <DisplayHeader />
      <main>
        <CoreConcepts />
        <Examples />
      </main>
    </>
  );
}

export default App;
```
````

<br>

`````ad-caution
title: Props are not forwarded to inner elements


````ad-quote
title: Header.jsx
icon: code

```
export default function Section({ title, children }) {
  return (
    <section>
      <h2>{title}</h2>
      {children}
    </section>
  );
}
```
````

<br>

![[Pasted image 20240214105859.png | center]]

When you are setting props on a custom component, those props are not automatically forwarded to the JSX code used inside of that component. Of course, we could now try to destructure the ID prop and then add it to the JSX manually.

That would work.

But when using this approach, we would have to destructure and manually set more and more attributes on this built-in section element. This is not scalable and not a convenient approach.

Therefore, we can use a pattern called **forwarded props** or **proxy props**.

````ad-quote
title: Section.jsx
icon: code

```
export default function Section({ title, children, ...props }) {
  return (
    // or <section {...props}>
    <section id={props.id}>
      <h2>{title}</h2>
      {children}
    </section>
  );
}
```
````
`````


<br>

### Common Prop Design Pattern

When creating components, reusability is a key concept. When logic gets grouped together with small components, this will subtract from its reusability.

`````ad-info
title: 
icon: code

````ad-quote
title: Tabs.jsx

```jsx
export default function Tabs({ children, buttons }) {
  return (
    <>
      <menu>{buttons}</menu>
      {children}
    </>
  );
}
```
````

<br>

````ad-quote
title: Examples.jsx
icon: code
collapse:

```jsx
import { useState } from "react";
import { EXAMPLES } from "../data";
import TabButton from "./TabButton";
import Section from "./Section";
import Tabs from "./Tabs";

export default function Examples() {
  const [selectedTopic, setSelectedTopic] = useState();

  function handleClick(selectedButton) {
    setSelectedTopic(selectedButton);
  }

  return (
    <Section title="Examples" id="examples">
      <Tabs
        buttons={
          <>
            <TabButton
              isSelected={selectedTopic === "components"}
              onClick={() => handleClick("components")}
            >
              Components
            </TabButton>
            <TabButton
              isSelected={selectedTopic === "jsx"}
              onClick={() => handleClick("jsx")}
            >
              JSX
            </TabButton>
            <TabButton
              isSelected={selectedTopic === "props"}
              onClick={() => handleClick("props")}
            >
              Props
            </TabButton>
            <TabButton
              isSelected={selectedTopic === "state"}
              onClick={() => handleClick("state")}
            >
              State
            </TabButton>
          </>
        }
      >
        <div id="tab-content">
          {!selectedTopic && <p>Please select a topic.</p>}
          {selectedTopic && (
            <>
              <h3>{EXAMPLES[selectedTopic].title}</h3>
              <p>{EXAMPLES[selectedTopic].description}</p>
              <pre>
                <code>{EXAMPLES[selectedTopic].code}</code>
              </pre>
            </>
          )}
        </div>
      </Tabs>
    </Section>
  );
}
```
````

When examining these two files, it may be tempting to remove the `buttons` property from the `Tabs` component and paste it into `Tabs.jsx`. The application would work the same, but `Tabs.jsx` would then be limited to likely 1 use-case. With it being seperated as it is, it would be simple to add another `Tabs` section to the website.

`````

<br>

### Setting Component Types Dynamically

Another important React concept to know is knowing how to set Component types dynamically. React allows you to pass a value for a prop which you can use inside of a component to dynamically render different HTML elements.

`````ad-info
title: 
icon: code

````ad-quote
title: Tabs.jsx
icon: code

```jsx
export default function Tabs({ children, buttons, ButtonsContainer = "menu" }) {
  return (
    <>
      <ButtonsContainer>{buttons}</ButtonsContainer>
      {children}
    </>
  );
}
```
````

<br>

````ad-quote
title: Examples.jsx
icon: code
collapse:

```jsx
return (
    <Section title="Examples" id="examples">
      <Tabs
        ButtonsContainer="menu" // or {Section} for custom components
        buttons={
          <>
            <TabButton
              isSelected={selectedTopic === "components"}
              onClick={() => handleClick("components")}
            >
              Components
            </TabButton>
            <TabButton
              isSelected={selectedTopic === "jsx"}
              onClick={() => handleClick("jsx")}
            >
              JSX
            </TabButton>
            <TabButton
              isSelected={selectedTopic === "props"}
              onClick={() => handleClick("props")}
            >
              Props
            </TabButton>
            <TabButton
              isSelected={selectedTopic === "state"}
              onClick={() => handleClick("state")}
            >
              State
            </TabButton>
          </>
        }
      >
        <div id="tab-content">
          {!selectedTopic && <p>Please select a topic.</p>}
          {selectedTopic && (
            <>
              <h3>{EXAMPLES[selectedTopic].title}</h3>
              <p>{EXAMPLES[selectedTopic].description}</p>
              <pre>
                <code>{EXAMPLES[selectedTopic].code}</code>
              </pre>
            </>
          )}
        </div>
      </Tabs>
    </Section>
  );
```
````
`````

<br>

## Not all content must go into components

`````ad-abstract
title:

In `index.jsx`, we are selecting the div with the ID root to then render the app component within the div. But what's really important to understand is that the index.html file is in the end the file that's going to be displayed to the visitors of your website.

Therefore, you can still add more markup to that file if needed.


````ad-quote
title: index.html
icon: code

```jsx
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/game-logo.png" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React Tic-Tac-Toe</title>
  </head>
  <body>
    <header>
      <img src="game-logo.png" alt="Hand-drawn tic tac tow game board" />
      <h1>Tic-tac-toe</h1>
    </header>
    <div id="root"></div>
    <script type="module" src="/src/index.jsx"></script>
  </body>
</html>
```
````
`````

<br>

## Where to store images

`````ad-abstract
title:

#### The public/ Folder

There are two options to store your images. The `public/` folder and the `src/assets` folder.

You can store images in the `public/` folder and then **directly reference** them from inside your `index.html` or `index.css` files.

The reason for that is that images (or, in general: files) stored in `public/` are made **publicly available** by the underlying project development server & build process. Just like `index.html`, those files can directly be visited from inside the browser and can therefore also be requested by other files.

If you try loading `localhost:5173/some-image.jpg`, you'll be able to see that image (if it exists in the `public/` folder).

<br>

#### The src/assets/ Folder

You can also store images in the `src/assets/` folder (or, actually, anywhere in the `src` folder).

Any files (of any format) stored in `src` (or subfolders like `src/assets/`) are **not made available to the public**. They can't be accessed by website visitors. If you try loading `localhost:5173/src/assets/some-image.jpg`, you'll get an error.

Instead, files stored in `src/` (and subfolders) can be used in your code files. Images imported into code files are then picked up by the underlying build process, potentially optimized, and kind of _"injected"_ into the `public/` folder right before serving the website. Links to those images are automatically generated and used in the places where you referenced the imported images.

<br>


#### Which Folder Should You Use?

You should use the `public/` folder for any images that should **not be handled by the build process** and that should be **generally available**. Good candidates are images used directly in the `index.html` file or favicons.

On the other hand, images that are used **inside of components** should typically be stored in the `src/` folder (e.g., in `src/assets/`).

`````


``````


## Advanced State Usage

```````ad-abstract
title: 


### Updating State Best Practices

It's important to remember that the `set` function that comes with `useState` is asynchronous. Meaning React will *schedule* the function to execute, instead of executing immediately. You can test this with simple boolean values:

````ad-quote
title: Player.jsx
icon: code

```jsx
import { useState } from "react";


export default function Player({ name, symbol }) {
  const [isEditing, setIsEditing] = useState(false);

  function handleClick() {
    setIsEditing(!isEditing); // => schedules a state update to true
    setIsEditing(!isEditing); // => schedules a state update to true
  }

  let playerName = <span className="player-name">{name}</span>;

  if (isEditing) playerName = <input type="text" required value={name} />;

  return (
    <li>
      <span className="player">
        {playerName}
        <span className="player-symbol">{symbol}</span>
      </span>
      <button onClick={handleClick}>{isEditing ? "Save" : "Edit"}</button>
    </li>
  );
}
```
````

It may seem as though the code above will do nothing, but that is not the case. On testing you'll see that the application runs as if the second `setIsEditing` doesn't exist.

<br>

````ad-question
title: Why is this the case?
collapse:

In React, state updates are asynchronous and are batched for performance reasons. When you call setState, React doesn't immediately update the state object; instead, it schedules an update to the component's state. This means that consecutive calls to setState within the same synchronous execution context may not see the updated state immediately.

In the provided code snippet, the function `handleClick` toggles the `isEditing` state twice in succession. However, since `setState` is asynchronous, both calls to `setIsEditing(!isEditing)` will use the same initial value of `isEditing`, which is `false` in this case.

Let's break down the sequence of events:

1. Initial render: `isEditing` is false.
2. User clicks the button triggering `handleClick`.
3. First call to `setIsEditing(!isEditing)`: `isEditing` is toggled to `true` and schedules a state update.
4. Second call to `setIsEditing(!isEditing)`: Again, `isEditing` is toggled to `true`, but this time, it's still based on the _initial_ value of `false`. It schedules another state update.

So effectively, both calls to `setIsEditing(!isEditing)` schedule an update to `true`, even though intuitively we might expect the second call to set the state back to `false`.

To avoid this issue, it's recommended to use the functional form of setState, which takes the previous state as an argument. This ensures that state updates are based on the latest state:

```js
function handleClick() {
  setIsEditing(prevIsEditing => !prevIsEditing);
}
```

With this change, React will correctly toggle the state regardless of the asynchronous nature of state updates.

````


<br>


### Two Way Binding

A common way to gain user input is through two way binding. It allows you to access values entered by a user into an `input` field and store the result into a state variable.

````ad-quote
title: Player.jsx
icon: code

```js
export default function Player({ initialName, symbol }) {
  const [isEditing, setIsEditing] = useState(false);
  const [playerName, setPlayerName] = useState(initialName);

  function handleClick() {
    setIsEditing((wasEditing) => !wasEditing);
  }

  function handleChange(e) {
    setPlayerName(e.target.value);
  }

  let editablePlayerName = <span className="player-name">{playerName}</span>;

  if (isEditing)
    editablePlayerName = (
      <input type="text" required value={playerName} onChange={handleChange} />
    );

  return (
    <li>
      <span className="player">
        {editablePlayerName}
        <span className="player-symbol">{symbol}</span>
      </span>
      <button onClick={handleClick}>{isEditing ? "Save" : "Edit"}</button>
    </li>
  );
}
```
````

<br>
<br>

### Best Practice: Updating Object State Immutably

``````ad-tip
title:

`````ad-quote
title: GameBoard.jsx
icon: code

```js
import { useState } from "react";

const initialGameBoard = [
  [null, null, null],
  [null, null, null],
  [null, null, null],
];

export default function GameBoard() {
  const [gameBoard, setGameBoard] = useState(initialGameBoard);

  function handleClick(row, col) {
    setGameBoard((oldGameboard) => {
      oldGameboard[row][col] = "X";
      return oldGameboard;
    });
  }

  return (
    <ol id="game-board">
      {initialGameBoard.map((row, i) => (
        <li key={i}>
          <ol>
            {row.map((playerSymbol, j) => (
              <li key={j}>
                <button onClick={handleClick}>{playerSymbol}</button>
              </li>
            ))}
          </ol>
        </li>
      ))}
    </ol>
  );
}
```
`````

<br>

When updating an objects state, it is strongly recommended to update that state in an immutable way. To do this, you just need to _create a copy of the old state_, and update the copy.

`````ad-question
title: Why is it important to maintain immutability in state?
collapse:

Maintaining immutability means to never directly mutate the state object. This is because React uses shallow comparison to determine if the state has changed and whether re-rendering is necessary. Mutating the state directly can lead to unpredictable behavior and bugs.

In the provided code, the `handleClick` function directly modifies the state object `oldGameboard` by assigning "X" to a specific position within it:

```js
oldGameboard[row][col] = "X";
```

This is problematic because it modifies the existing state object in-place, violating the principle of immutability. React won't recognize this as a state update because it relies on shallow comparison to detect changes. *Since the state object remains the same reference after mutation, React won't trigger a re-render*, leading to UI inconsistencies and bugs.

To ensure immutability, you should create a new copy of the state object with the necessary modifications. This can be achieved using methods like `map`, `slice`, or spread syntax (`...`).

````ad-quote
title: Updated With Immutability
icon: code

```js
function handleClick(row, col) {
	setGameBoard((oldGameboard) => {
	  const updatedBoard = [...oldGameboard.map((row) => [...row])];
	  updatedBoard[row][col] = "X";
	  return updatedBoard;
	});
}
```
````
`````


![[Pasted image 20240216150508.png | center | 1500]]

``````

<br>
<br>


### Lifting State Up

In the `GameBoard` component, we need the symbol of the active player. And in the `Player` component, we want to add a CSS class to the list item dynamically. That's of course a problem because these are two separate components.

How can we make sure that they both have access to the information which player is currently active?

Well, in common cases like this, we need to do something which is called ***lifting the state up***.

Instead of managing the information which player is currently active in the `GameBoard` or the `Player` component, we need to manage the state in the closest ancestor component that has access to both components that need that information.

![[Pasted image 20240220123917.png | center]]

So in this case, the `App` component. Because the `App` component can then pass the information which player is currently active to both the `Player` and the `GameBoard` components via props.

````ad-code
title: App.jsx
collapse: 

```js
import { useState } from "react";
import Player from "./components/Player";
import GameBoard from "./components/GameBoard";

function App() {
  const [activePlayer, setActivePlayer] = useState("X");

  function handleSquareClick() {
    setActivePlayer((curActivePlayer) => (curActivePlayer === "X" ? "O" : "X"));
  }

  return (
    <main>
      <div id="game-container">
        <ol id="players" className="highlight-player">
          <Player
            initialName="Player 1"
            symbol="X"
            isActive={activePlayer === "X"}
          />
          <Player
            initialName="Player 2"
            symbol="O"
            isActive={activePlayer === "O"}
          />
        </ol>
        <GameBoard onSquareClick={handleSquareClick} symbol={activePlayer} />
      </div>
      LOG
    </main>
  );
}

export default App;

```
````

<br>

````ad-code
title: Player.jsx
collapse: 

```js
import { useState } from "react";

export default function Player({ initialName, symbol, isActive }) {
  const [isEditing, setIsEditing] = useState(false);
  const [playerName, setPlayerName] = useState(initialName);

  function handleClick() {
    setIsEditing((wasEditing) => !wasEditing);
  }

  function handleChange(e) {
    setPlayerName(e.target.value);
  }

  let editablePlayerName = <span className="player-name">{playerName}</span>;

  if (isEditing)
    editablePlayerName = (
      <input type="text" required value={playerName} onChange={handleChange} />
    );

  return (
    <li className={isActive ? "active" : undefined}>
      <span className="player">
        {editablePlayerName}
        <span className="player-symbol">{symbol}</span>
      </span>
      <button onClick={handleClick}>{isEditing ? "Save" : "Edit"}</button>
    </li>
  );
}
```
````

<br>

````ad-code
title: GameBoard.jsx
collapse:

```jsimport { useState } from "react";

const initialGameBoard = [
  [null, null, null],
  [null, null, null],
  [null, null, null],
];

export default function GameBoard({ onSquareClick, symbol }) {
  const [gameBoard, setGameBoard] = useState(initialGameBoard);

  function handleClick(row, col) {
    setGameBoard((oldGameBoard) => {
      const updatedBoard = [...oldGameBoard.map((row) => [...row])];
      updatedBoard[row][col] = symbol;
      return updatedBoard;
    });

    onSquareClick();
  }

  return (
    <ol id="game-board">
      {gameBoard.map((row, i) => (
        <li key={i}>
          <ol>
            {row.map((playerSymbol, j) => (
              <li key={j}>
                <button onClick={() => handleClick(i, j)}>
                  {playerSymbol}
                </button>
              </li>
            ))}
          </ol>
        </li>
      ))}
    </ol>
  );
}

```
````

<br>

### Deriving State From Props

````ad-code
title: App.jsx
collapse:

```js
import { useState } from "react";
import Player from "./components/Player";
import GameBoard from "./components/GameBoard";
import Log from "./components/Log";

function App() {
  const [gameTurns, setGameTurns] = useState([]);
  const [activePlayer, setActivePlayer] = useState("X");

  function handleSquareClick(rowIndex, colIndex) {
    setActivePlayer((curActivePlayer) => (curActivePlayer === "X" ? "O" : "X"));
    setGameTurns((prevTurns) => {
      let currentPlayer =
        prevTurns.length > 0 && prevTurns[0].player === "X" ? "O" : "X";

      const updatedTurns = [
        {
          square: { row: rowIndex, col: colIndex },
          player: currentPlayer,
        },
        ...prevTurns,
      ];

      return updatedTurns;
    });
  }

  return (
    <main>
      <div id="game-container">
        <ol id="players" className="highlight-player">
          <Player
            initialName="Player 1"
            symbol="X"
            isActive={activePlayer === "X"}
          />
          <Player
            initialName="Player 2"
            symbol="O"
            isActive={activePlayer === "O"}
          />
        </ol>
        <GameBoard onSquareClick={handleSquareClick} turns={gameTurns} />
      </div>
      <Log turns={gameTurns} />
    </main>
  );
}

export default App;
```
````

<br>

````ad-code
title: GameBoard.jsx
collapse:

```js
const initialGameBoard = [
  [null, null, null],
  [null, null, null],
  [null, null, null],
];

export default function GameBoard({ onSquareClick, turns }) {
  let gameBoard = initialGameBoard;

  for (const turn of turns) {
    gameBoard[turn.square.row][turn.square.col] = turn.player;
  }

  return (
    <ol id="game-board">
      {gameBoard.map((row, i) => (
        <li key={i}>
          <ol>
            {row.map((playerSymbol, j) => (
              <li key={j}>
                <button
                  onClick={() => onSquareClick(i, j)}
                  disabled={gameBoard[i][j] !== null}
                  style={{ cursor: gameBoard[i][j] === null && "pointer" }}
                >
                  {playerSymbol}
                </button>
              </li>
            ))}
          </ol>
        </li>
      ))}
    </ol>
  );
}
```
````

<br>

```ad-tip
title:

Deriving state from props is a common pattern in React that involves using the initial props passed to a component to calculate its internal state. This pattern is especially useful when the component's state can be determined solely based on the props it receives, avoiding the need to duplicate data and reducing complexity.

In the provided example, the `GameBoard` component receives two props: `onSquareClick` and `turns`. The `turns` prop contains an array of objects representing the history of moves in the game, while the `onSquareClick` prop is a function to handle square clicks.

Instead of storing the game board state directly as a component state, the `GameBoard` component derives its state from the `turns` prop. This means that the component doesn't need to maintain its own separate state to represent the game board; instead, it calculates the current state of the game board based on the props it receives.

By deriving state from props, the `GameBoard` component follows the principle of managing minimal state. It avoids duplicating data and ensures that the component's state is always consistent with the external source of truth (in this case, the `turns` prop). This approach leads to cleaner and more predictable code, as the component's behavior is directly tied to the data it receives.

Deriving state from props is a powerful pattern in React for managing component state efficiently and maintaining consistency with external data sources. It promotes code simplicity, reusability, and better separation of concerns.

```


```````

---
Created: January 5, 2024
Last Modified: `= this.file.mtime`
