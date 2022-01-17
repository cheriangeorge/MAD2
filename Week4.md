### Week 4 Notes

#### Vue
* Declarative Rendering - Phrase popularised by vue
  - Reactivity 
  - Directives
  - Event handling
  - Class and Style binding
  - Lists and Loops

* Reactivity 
  - Auto update in response to changes in data
  - Binding between model (data) and view (display)
  - Focus on What instead of How in declerative programming - key to understanding philosophy behind vue.
* Why ?
  - User interaction is fundamentally reactive
    - Respond to changes in input
  - Change in one parameter may need multiple updates on screen
    - User logs in
    - Update navigation : add logged in links
    - Update displayed list of courses
    - Change colours based on theme
  - CPUs are fundamentally imperative - ie : you have to give it every step.
 * How?
  - Server tracks state
    - user logged in
    - date/time
    - Server knows exactly what is happening
  - Server responds with complete HTML based on persent state
    - Capture different layouts, visibility in views
    - Render appropriately for each user
    - Fully server side
  - Client JS
    - Login controller retreives user model
    - Client side JS goes through each element and updates as needed (jQuery, Vanilla JS)

* Vue - directives
  - v-bind : one way binding - update variable , reflects on display
    - v-model: two way binding -inputs,checkboxes, form data
  - v-on : event binding
    - most common form is `v-on:click`
  - Changes in the model reflects on the display and changes in the actions to reflect in the model.
* Class binding
  - Dynamically modify class of an object
  - Special support for bind - object
  - Multiple classes attached based on key-values
    - If value for a given key is true, that key is applied as a class or style.
* Conditional rendering
  - `v-if="argument"`
    - what follows is shown when argument evaluates to true
    - JS based - changes DOM
  - `v-show="param"`
    - only if the show parameter evaluates to true
    - always rendered and present in DOM - only CSS display parameter changed
* Looping
  - Iterate over any JS iterable
    - Array , Object, String etc..
  - Usage similar to Jinja {{}} templates
  - Examples :
    - `v-for="item in items"` // items in an array
    - `v-for="value in obj"` // obj is an object
    - `v-for="(value, name) in obj"` // name -> key : "key" has another meaning in v-for
    - `v-for="(value, name, index) in obj"` // index -> numerical index

* Loop Keys 
  - Looping creates DOM elements
    - vue needs some way to keep track of elements if updating needed
    - Virtual DOM "diffing" used to find what changes refelect on screen
    - Vue uses heuristics to see what can be minimised
  - For simple updates simple heuristics are sufficient
    - For more complex updates, may not be as easy to track what has changed or what is new
  - Provide a "key"
    - Key must be unique for each loop element
    - Updating item with same key will automatically update only relevant items
  - Rule of thumb : provide a key whereever possible- index, ID

#### Demo
* Javascript essentially treats a function and variable as the same 


___

### Live session video
[Week 4 Live session on Monday 17th Jan 2022](https://www.youtube.com/watch?v=faRuwqZV--w)
