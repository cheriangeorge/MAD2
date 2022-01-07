## Week 2 Notes

### Javascript Collections 
* Arrays
  - Basic arrays are a collection of objects of any type
      - Can even be mixed type (numbers,strings,objects,functions)
  - Element Access
  - Length
  - Holes
  - Iteration
* Synchronous Iteration 
  - Go over all the elements in a collection
  - Concepts :
      - **Iterable** - an object whose contents can be accessed sequentially 
      - **Iterator** - pointer to the next element
  - Iterable Objects :
      - Array
      - String
      - Map
      - Set
      - Browser DOM - tree structure
   - Objects : `object.keys()` and `object.entries()` - helper functions
* Multi-dimensional
  - Iterations and Transformations
    - ***Functions that take functions as input***
    - `map`, `filter`, `find`
      - Apply a callback function over each element of array
    - Elements of functional programming: create a transformation chain
    - Callback: important concept - function passed in to another function, to be called back for some purpose
* Maps, Sets ..
  - Other collections 
    - Maps : Proper dictionaries instead of objects
    - WeakMaps
    - Sets
  - Use only if needed
* Destructuring
  - Simple syntax to split an array into multiple variables
  - Easier to pass and collect arguments etc.
  - Also possible for objects
* Generators
  - Functions that yield values one at a time
  - Computed iterables
  - Dynamically generate iterators

### Modularity 
* Modules
  - Collect related functions, objects, values together
  - “export” values for use by other scripts
  - “import” values from other scripts, packages
* Ways of implementing
  - script - direct include script inside browser
  - CommonJS - introduced for server side modules
    - synchronous load: server blocks till module loaded
  - AMD - asynchronous module definition
    - browser side modules
  - ECMAScript 6 and above:
    - ES6 Modules
      - Both servers and browsers
      - Asynchronous load
* npm
  - Node Package Manager
  - Node:
    - command line interface for JS
    - Mainly used for backend code, can also be used for testing
  - npm can also be used to package modules for frontend
    - “Bundle” managers - webpack, rollup etc.
* Objects
  - Everything is an object …
  - Object literals
    - Assign values to named parameters in object
  - Object methods
    - Assign functions that can be called on object
  - Special variable `this`
  - Function methods
    - `call()`, `apply()`, `bind()`
  - `Object.keys()`, `values()`, `entries()`
    - use as dictionary
    - iterators
  - Prototype based inheritance
    - Object can have a “prototype”
    - Automatically get properties of parent
    - Single inheritance track
  - Class
    - Better syntax - still prototype based inheritance
    - constructor must explicitly call `super()`
    - Multiple inheritance or **Mixins**
      - Complex to implement - out of scope here
