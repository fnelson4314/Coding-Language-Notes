# ReactJS

## Getting started

- To get a basic react project and the needed files, run **rpm create vite@latest**
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
```js
const [age, setAge] = useState(0);

const incrementAge = () => {
  setAge(age + 1);
}
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


