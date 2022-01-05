## Week 1 Notes from Slides and Lectures 

### Javascript History
* Originally created in 1995 as scripting language for Netscape Navigator
* Intended as “glue” language
* Primarily meant to assist “applets” in Java - hence JavaScript
* AJAX - Asynchronous Javascript and XML (Garrett 2005) - Google Maps, Google Suggest loads only what is needed.

### ECMA script
* Standard for Javascript - ECMA (European Computer Manufacturers Association) - standard 262
* JAM Stack - Javascript APIs Markup
* Called ECMAScript to avoid trademark issues with Java
* Yearly releases since 2015 (ES 6)
* ES 6 has features of modern languages - Like modules, scoping, class
* What happens if browsers don't support these features 
  - Ask user to upgrade
  - Package browser and application together (VSCode - Electron)
  - Polyfills : libraries that emulate newer functionality for older browsers
  - Compilers: BabelJS - convert new code to older compatible versions
* Javascript Engines
  - **V8** from Google is the most used JavaScript engine
  - **SpiderMonkey** is developed by Mozilla for use in Firefox 
  - **JavaScriptCore** is Apple's engine for its Safari browser
  - **Chakra** is the engine of the Internet Explorer and Edge browser.

### Features of Javascript
* Highly tolerant of errors
  - Debugging difficult
  - Strict mode: “use strict”;
* Ambiguous syntax variants
  - Automatic semicolon insertion
  - ?? Object literals vs Code blocks {}
  - ?? Function: statement or expression? Impacts parsing
* Limited IO support: errors “logged” to “console”
* Closely integrates with presentation layer: DOM APIs
* Asynchronous processing and the Event Loop
* Need HTML file to load the JS as a script though NodeJS allows execution from command line

### Javascript Syntax 
* Basic Javascript for the Frontend
  - Scripting language so no compilation step
  - Loosely structured 
* Identifiers 
  - Reserved words (await, break, class etc...)
  - Literals (values) : true, false, null
* Statements and Expessions 
  - Statement is a piece of code that can be executed
  - Expression is code that can be excuted to get a value to be returned
* Data Types
  - Primitive data types - undefined, null, boolean, number, string, bigint, symbol 
  - Objects - Compound pieces of data
  - Functions - can be handled like objects, objects can have functions / methods, functions can also have objects
* Strings
  - Source code is expected to be in unicode. Most engines use UTF 16
  - Functions like length can give surpeising results on non-ASCII scripts
* Non Values 
  - undefined - usually implies not initialised and is the default unknown state
  - null - explicitly set non-value
* Operators and comparisons 
  - Addition, subtraction - numbers and strings
  - Coersion - convert to similar type where operation is defined 
  - Comparison - == loose equality , ===  strict equality
* Variables and Scoping
  - let, const are used for declaring variables
  - Unlike Python, variables MUST be declared
  - Unlike C, their type need NOT be declared
  - var was originally used for declaring variables, but has function level scope - avoid
  - const : declares an immutable object - Value cannot be changed once assigned - But only within scope
  - let: variable that can be updated - index variable in for loops
* Control Flow
  - Conditional execution - if, else
  - Iteration - for, while
  - Change in flow - break, continue
  - Choice - switch
* Functions
  - Reusable block of code
  - In javascript functions are themselves objects that can be assigned
  - can take parameters or arguments and perform a computation
* Anonymous functions and IIFEs
  - Immediately Invoked Function Expression
  - IIFE was used before let and const to create strict scoping  - Avoid using
  - let x = function () { return “hello”} // Anonymous bound
  - (function () { return “hello” }()) // Declare and invoke
  - Avoid IIFEs in modern code - poor readability
* console.log
  - it is very limited
  - variants for error logging
  - useful for limited form of debugging. Not for production.
#### Function Notation
* Regular Decleration
```Javascript
function add(x, y){
  return x + y;
}
// Statement
```
* Named Variable
```javascript
let add = function(x, y) {
  return x + y;
}
// Expression
```
* Arrow Function
```javascript
let add =
(x, y) => x + y;
// Expression
```
### DOM API
* JS was designed for document manipulation
* Inputs from DOM: mouse, text, clicks
* Outputs to DOM: manipulation of text, colours etc.

### Javascript notes from AQs and Live sessions
* UTF 16 in Javascript - can use different scripts as variable names
* console.log()
  - by default last statement gets printed in colsole even if there is no console.log
  - if there is no let/var/const present it will be printed in the console.
* {} is a block 
* var - even if defined inside a block it is visible outside. The entire top-level script can see it.
* let - Later versions of javascript brought it because var was difficult to scope. Allows more restrictive scoping. **ReferenceError** if we try to access a variable declared by let inside a block, outside the block.
  - let allows you to declare variables that are limited to the scope of a block statement, or expression on which it is used, unlike the var keyword, which declares a variable globally, or locally to an entire function regardless of block scope. [Mozilla Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
* const - works exactly like let - block level scope . Should be used in most places. Cannot be changed.
* Avoid using var.
* scope of a variable
* Namespaces to restrict how different names are seen to different parts of the code 
* Zero indexing of strings and arrays
* String .length .substring
* Length of a string not clearly defined when it is in unicode
* Template string
  - contained within back ticks <code>\` \`</code>
  - <code>let st = \`${s} World!\`</code>
  - <code>console.log(\`Fifteen is ${a + b} and not ${2 * a + b}.\`);</code>
* Operators 
  - 3+4 
  - '3'+'4'
  - '3' + 4 (coersion - converts 4 into a string)
  - '3' * '4' - 12
  - Don't use coersion in production code - creates confusion
  - console.log('3' == 3) outputs true
  - Use Strict equality **===** to avoid coersion. Safer to use for comparisons.
* Backtick is below the tilda on the keyboard (` is not the same as ')
### Scoping
* Hoisting - It is a Javascript mechanism where variables and function declarations are moved to the top of their scope before code execution.
### 'this' works differently within an arrow function

```javascript

const obj = {
  name : 'Rohit',
  arrowFunction : (x) => {
    this.name = x;
  },
  normalFunction : function (x) {
    this.name = x;
  },
}
console.log(obj.name) // prints Rohit
obj.arrowFunction('Mohit');
console.log(obj.name) // prints Rohit
obj.normalFunction('Mohit');
console.log(obj.name) // prints Mohit

// 'this' works differently within an arrow function

```

### Timeout depends on processor
```Javascript
const timer = (time) => {
  let x = 1;
  let handlar = setInterval(()=>{
    console.log(2*x)
    x++
  }, 1000)

  setTimeout(()=>{
    clearInterval(handlar)
  }, time)
}
timer(5004) // Will display up to 8 in some cases Increase it by a few ms to display upto 10.
```

### Hoisting of var,let and const
```Javascript
let a = 9;
{
  console.log(a);
  // let a = 5; // gives ReferenceError 
  // split into let a ; a =5
  // let a gets 'hoisted' to the parent scope
  // the default value becomes undefined
  // var a = 5 // Does not give an error
  // For var the variables will get initialised with undefined value after hoisting. For let and const, it does not get un-initialised.
  a = 5 // prints 5 in the console
}
```
* var will be hoisted to global scope when declared
* let and const will not be hoisted to global scope
