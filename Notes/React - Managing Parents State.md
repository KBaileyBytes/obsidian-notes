---
tags:
  - note
---
# `=this.file.name`
---

````ad-code
title: App.jsx

```jsx
import SideBar from "./components/SideBar";
import Button from "./components/Button";
import image from "./assets/no-projects.png";
import { useState } from "react";

function App() {
  const [projects, setProjects] = useState([]);
  const [isOpen, setIsOpen] = useState(false);

  const toggleForm = () => {
    setIsOpen((oldState) => !oldState);
  };

  return (
    <div className="flex h-screen mt-8">
      <SideBar toggleForm={toggleForm} />
      <div className={isOpen.toString()}></div>
      <div
        className="w-full flex flex-col items-center p-4 my-8"
        id="main-content"
      >
        <img src={image} alt="pic" className="w-52" />
        <p className="text-xl py-6">No Project Selected</p>
        <Button onClick={toggleForm}>Create new project</Button>
      </div>
    </div>
  );
}

export default App;
```
````

````ad-code
title: SideBar.jsx

```jsx
import Button from "./Button";

export default function SideBar(props) {
  return (
    <div className="bg-black p-8 rounded-tr-lg w-96">
      <p className="my-8 text-2xl font-bold uppercase text-white">
        Your Projects
      </p>
      <Button onClick={props.toggleForm}>+ Add Project</Button>
    </div>
  );
}
```
````


---
Created: March 26, 2024
Last Modified: `= this.file.mtime`
