# ReactJS

## Getting started

- To get a basic react project and the needed files, run **npm create vite@latest**
- Enter your project name
- Select the React framework
- Then select Javascript 
- Follow the rest of the install instructions

## React project structure

- npm_modules - Contains external libraries that our project relies on
- public - Folder that contains any public assets like public fonts, images, videos, etc.
- src - Where all of our code will be written in

## Components

- A component can be created in a file of its own and can be inserted repeatedly in other files
```js
function Header() {
  return(
    <header>
      <h1>My website</h1>
    </header>
  );
}

export default Header
```

- This can then be inserted in other files by first importing the component, then used like **\<Header>\</Header>** or shorthand **\<Header/>**
- For jsx, when returning you can only return one element. So if you want multiple components, this can be easily fixed by adding in empty angle brackets (\<>\</>)
- If you'd like to add some javascript in the return statement, this must be surrounded by curly brackets. If just inside the function and not the return statement, you don't need curly brackets
- With jsx, "class" is a reserved keyword so use "className" instead

## Click events

- When creating a button element, there's an "onClick" option available where a function can be assigned to run when a user clicks the button
  - There's also an "onDoubleClick" option
```js
function Button() {
  const handleClick = (name) => console.log(`${name} stop clicking me`);

  return(<button onClick={() = handleClick("Bro")}Click me</button>
}
export default button
```
- If the callback function has a parameter, you must use an arrow function to call it
- Every click event automatically comes with an "event" parameter that can be used
  - This event object has many different properties that can be used. You can see these properties by logging the event to the console
 
## React hooks

- The most common react hook is the "useState" hook. This allows the creation of a stateful variable and a setter function to update its value in the Virtual DOM. [name, setName]
  - To use it, do "import React, {useState} from 'react';"
  - The stateful variable can only be changed using the given setter function as nothing would happen if you tried to assign a value directly to the stateful variable
  - You can pass in a default value to useState for when the variable hasn't been set yet
  - If the variable ends up being an object or an array and you'd like to add or modify, you can do something like **setFoods(f => [...f, newFood]); The ...f holds everything that was already in the object/array and the newFood is the thing you'd like to add
```js
const [age, setAge] = useState(0);

const incrementAge = () => {
  setAge(age + 1);
}
```

- Another common react hook is "useEffect". This tells React to DO SOME CODE WHEN this component re-renders, this component mounts, the state of a value changes:
  - useEffect(() => {}) runs after every re-render
  - useEffect(() => {}, []) runs only on mount
  - useEffect(() => {}, [value]) runs on mount + when value changes
  - Uses:
    - Event listeners
    - DOM manipulation
    - Subscription (real-time updates)
    - Fetching Data from an API
    - Clean up when a component unmounts
```js
const [count, setCount] = useState(0);

useEffect(() => {
  document.title = `Count: ${count}`;
}, [count]); // This automatically updates the title upon rendering as well as whenever count changes since it's in the dependencies
```

## onChange

- The onChange event handler triggers a function every time the value of the input changes. Primarily used with form elements like \<input>, \<select>, \<textarea>, etc.
```js
const [name, setName] = useState("Guest");

function handleNameChange(event) {
  setName(event.target.value);
}

return(<div>
          <input value={name} onChange={handleNameChange}/>
);
```

## Page routing

- The main page router paired with react is React Router Dom
- This can be installed with **npm i react-router-dom**
- To use it in your code do **import { BrowserRouter, Routes, Route, useNavigate } from "react-router-dom";**
  - BrowserRouter is the top level router for web apps that will wrap everything
  - Routes will wrap all of your Route components
  - Route defines a path and component to render
    - Need to provide some attributes
    - path for what you'd like the url path to be for your component
    - element to specify your component to render
  - useNavigate allows you to redirect to another page usually after some sort of action
    - ```js
      const navigate = useNavigate();
      return navigate('/jobs');
      ```
    
```js
return (
  <div className="app">
    <BrowserRouter>
      {!user ? (
        <LoginScreen />
      ) : (
        <Routes>
          <Route path="/profile" element={<ProfileScreen />} />
          <Route path="/" element={<HomeScreen />} />
        </Routes>
      )}
    </BrowserRouter>
  </div>
);
```

## Async functions and fetching data

- In JavaScript, operations like fetching data from an API, reading a file, or waiting for a timeout don’t return results immediately — they return a Promise. async/await is a way to write asynchronous code that looks synchronous, making it easier to understand and debug.
- Using async for a function makes sure that a function always returns a promise
- Using await pauses execution inside an async function until the promise is resolved
```js
async function getData() {
  try {
    const response = await fetch('/data');  // Waits for fetch to finish
    const data = await response.json();     // Waits for JSON to parse
    console.log(data);
  } catch (error) {
    console.error('Something went wrong:', error);
  }
}
```

- To post data, you can do a POST request
```js
const addJob = async (newJob) => {
  const res = await fetch("/api/jobs", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(newJob),
  });
  return;
};
```
