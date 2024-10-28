# JavaScript and Axios Cheat Sheet 📜

A quick reference guide to essential JavaScript features and using `axios` for API calls.

---

## Table of Contents
- [JavaScript Basics](#javascript-basics)
- [Functions](#functions)
- [ES6+ Features](#es6-features)
- [Working with Arrays](#working-with-arrays)
- [Promises and Async/Await](#promises-and-asyncawait)
- [Axios for API Calls](#axios-for-api-calls)

---

## JavaScript Basics
### Variables
```javascript
let x = 10; // Block-scoped
const y = 20; // Constant, block-scoped
var z = 30; // Function-scoped
Data Types
Primitive: string, number, boolean, null, undefined, symbol, bigint
Non-Primitive: object, array, function
Conditional Statements
javascript
Copy code
if (condition) { ... } 
else if (condition) { ... }
else { ... }
Loops
javascript
Copy code
for (let i = 0; i < 5; i++) { ... } // Standard for-loop
while (condition) { ... } // While-loop
array.forEach(item => { ... }); // Array iteration
Functions
Function Declaration
javascript
Copy code
function add(a, b) { return a + b; }
Arrow Functions
javascript
Copy code
const multiply = (a, b) => a * b;
Default Parameters
javascript
Copy code
function greet(name = "Guest") { console.log("Hello, " + name); }
Rest and Spread Operators
javascript
Copy code
function sum(...args) { return args.reduce((acc, val) => acc + val, 0); }
let arr = [1, 2, 3];
let newArr = [...arr, 4, 5];
ES6+ Features
Destructuring
javascript
Copy code
const person = { name: 'John', age: 30 };
const { name, age } = person; // Object destructuring
const arr = [1, 2, 3];
const [first, second] = arr; // Array destructuring
Template Literals
javascript
Copy code
const name = "Alice";
console.log(`Hello, ${name}!`);
Classes
javascript
Copy code
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
const john = new Person("John", 30);
Modules
Exporting: export function foo() { ... }
Importing: import { foo } from './module.js';
Working with Arrays
Method	Description	Example Usage
map()	Transforms each array element	arr.map(num => num * 2);
filter()	Filters elements based on condition	arr.filter(num => num > 10);
reduce()	Reduces array to a single value	arr.reduce((a, b) => a + b);
find()	Finds the first match	arr.find(num => num > 10);
Promises and Async/Await
Promise
javascript
Copy code
const promise = new Promise((resolve, reject) => {
  if (success) resolve("Done!");
  else reject("Error!");
});
promise.then(result => console.log(result)).catch(error => console.log(error));
Async/Await
javascript
Copy code
async function fetchData() {
  try {
    const result = await someAsyncFunction();
    console.log(result);
  } catch (error) {
    console.error(error);
  }
}
Axios for API Calls
Install axios
bash
Copy code
npm install axios
Basic GET Request
javascript
Copy code
import axios from 'axios';
axios.get('https://api.example.com/data')
  .then(response => console.log(response.data))
  .catch(error => console.error(error));
POST Request
javascript
Copy code
axios.post('https://api.example.com/data', { key: 'value' })
  .then(response => console.log(response.data))
  .catch(error => console.error(error));
Setting Headers
javascript
Copy code
axios.get('https://api.example.com/data', {
  headers: { Authorization: 'Bearer token' }
});
Using Async/Await with Axios
javascript
Copy code
async function fetchData() {
  try {
    const response = await axios.get('https://api.example.com/data');
    console.log(response.data);
  } catch (error) {
    console.error(error);
  }
}
Additional Tips
Preview before committing: Use GitHub’s Markdown preview to make sure everything renders as expected.
Consider adding syntax highlighting: Code blocks with ```javascript provide better readability.
Icons for readability (optional): Emojis can be used sparingly to make headers or important points more visual.
Use whitespace and horizontal lines (---) for clear sections.
This cheat sheet provides core concepts and common uses of JavaScript and Axios for quick reference.

typescript
Copy code

You can save this content as a `.md` file, and it will be formatted nicely on GitHub! Let me know if you need any further modifications or additions.





