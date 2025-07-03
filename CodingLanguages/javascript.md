# Javascript

## Basics to start

- console.log() is like a print statement in other languages and prints output to the terminal
- Programs can be run using node by doing **node fileName**


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
- object: Hold key value pairs and can hold many different data types. A dictionary
  - **let person = { name: "John", hours: 3 }**

