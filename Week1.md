### ECMA script
* Standard for Javascript

### Javascript
* UTF 16 in Javascript - can use different scripts as variable names
* console.log()
  - by default last statement gets printed in colsole even if there is no console.log
  - if there is no let/var/const present it will be printed in the console.
* {} is a block 
* let
* const
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
  - contained within back ticks ' ' 
  - let st = '${s} World!'
* Operators 
  - 3+4 
  - '3'+'4'
  - '3' + 4 (coersion - converts 4 into a string)
  - '3' * '4' - 12
  - Don't use coersion in production code - creates confusion
  - console.log('3' == 3) outputs true
  - Use Strict equality **===** to avoid coersion. Safer to use for comparisons.
### Scoping
* Hoisting - It is a Javascript mechanism where variables and function declarations are moved to the top of their scope before code execution.
### Strings 
* Strings usually use UTF-16 encoding
* Functions like length can give surprising results on non-ASCII strings
* **Non Values**
  - Undefined - Usually implies not initialised ; Default unknown state 
  - Null - Explicitly set to non-value
  - May be used interchangibly in most places

* Anonymous functions and IIFEs
  - IIFE was used before let and const to create strict scoping  - Avoid using
  - Immediately Invoked Function Expression
  - When to use ?
 * console.log(typeof(x))
 * Functions can have objects within them
 * 

### DOM API
* console.log
  - it is very limited
  - variants for error logging
  - useful for limited form of debugging. Not for production.

* Backtick is below the tilda on the keyboard (` is not the same as ')
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
