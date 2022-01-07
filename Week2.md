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
