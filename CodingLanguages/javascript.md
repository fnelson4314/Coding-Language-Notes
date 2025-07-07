# Javascript

## Basics to start

- console.log() is like a print statement in other languages and prints output to the terminal
- Programs can be run using node by doing **node fileName**
- To include a javascript script file in an html file, you can add **\<script src="filename.js">\</script>**


## Variables

- The main data type used in javascript is **let**. The let keyword is used for variables which hold values that CAN be changed
  - **let firstName = 'Steven';**
- The **const** keyword is used for declaring variables which hold values that CANNOT be changed. The common convention for naming these is using all uppercase
  - **const COLOR_GREEN = 'green';**

## Data types

- Strings: You can declare a string in three different ways
  - **let favoriteFruit = 'strawberry';**
  - **let favoriteIceCream = "chocolate";**
  - **let favoriteProgrammingLaguage = `JavaScript`;**
- Number: Encompasses integers and decimal values
- BigInt: Allows you to work with integers larger than 2^53 - 1. Used by appending an n to the end of the integer
  - **let veryLargeNumber = 39485734895739n;**
- boolean: Stores true or false
- undefined: When you assign a variable without initializing
- null: Used to clear the value of a variable
- Symbol: Used to create unique identifiers and objects
  - **const uniqueKey = Symbol();**
- object: Can hold many different data types
  - **let person = { name: "John", hours: 3 }**
  - Array: **let colors = ['red', 'blue']
    - Can use **.length** to get the length of an array


## Functions

Sample function and calling that function:
```javascript
function sayHi(name) {
  console.log('Hi!' + name);
}

sayHi('Steven');
```

A constructor function can be used to create an object. It is called with the **new** keyword:
```javascript
function Dog(name, breed, age, weightInPounds) {
  this.name = name;
  this.breed = breed;
  this.age = age;
  this.weightInPounts = weightInPounds;
  this.eat = function() {
    console.log(this.name + ': Chomp!');
  }

  this.bark = function() {
    console.log(this.name + ': Woof!');
  }
}

const anotherDog = new Dog('Marley', 'Lab', 3, 60);
```

Another very important type of function is the arrow function. It is often used as a shorter version of common functions

- **let sum = (a, b) => a + b;**
- Can be multiline as well but this will need an explicit "return":
```javascript
let sum = (a, b) => {
  let result = a + b;
  return result;
};
```

## Common functions

- .map(): The .map() function is used to map a function to each element in the provided array
  - const mappedArr = arr.map((num) => num + 1);
- .filter(): Similar to .map() but it expects a callback function that returns true or false and only outputs the items that returned true

## Importing and Exporting

Exporting a variable from a file can be done in two ways

- It can be done using a named export like **export const greeting = "Hello, Odinite!";**
  - Or it can be done separately by exporting multiple variables at once by putting it at the end like **export { greeting, farewell };**
- You can also do a default import which can only be used on a single thing for a file by adding it at the end of a file like **export default "Hello, Odinite!";**
  - You can mix named and default exports, but you can only have one default export per file. People tend to use this when they only have a single function/variable in their file

Importing can easily be done by picking and choosing what variables/function from what file

- **import { greeting, farewell }  from "./one.js";** for named exports
- **import helloOdinite from "./one.js"** for default exports
- **import greeting, { farewell } from "./one.js"** for mixed exports

When adding a script to a file, you can do **\<script src="two.js" type="module">\</script>** if two.js imports from another script and depends on it. This makes it so you don't have to add a script for one.js as well

## Working with the DOM

The DOM is the Document Object Model and is like a tree of "nodes" full of all the components of an html file.

There are many DOM methods that can be used: 
