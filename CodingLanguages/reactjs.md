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
- 
