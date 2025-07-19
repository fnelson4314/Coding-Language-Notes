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
