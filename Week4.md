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
