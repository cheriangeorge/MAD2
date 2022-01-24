### Week 5 Notes

#### Using APIs 
* Separation of concerns
  - Backend : manage data models
  - Frontend : manage UI (The part closer to the user)
  - A clean interaction mechanism to separate the two
* Requirements of such a system
  - System level design should have a separate backend and front end 
    - Backend should never know what the UI looks like (Separation of concerns for abstraction)
    - No direct calls to HTML tempeplate rendering etc.
    - Data output only in neutral formats : JSON is preferred nowadays, but not essential
    - Data input through form data or URLs
  - Fetch Mechanism
    - How to retreive data from a backend?
    - URL based APIs (REST)
  - Rendering mechanism 
    - Frontend can be rendered on server and pushed
    - Frontend implemented in browser, pulls data (Vue)
* Fetch  - Asynchronous
  - Fetching data depends on factors outside server control
    - Latency to backend (network disruption)
    - Network load, disruptions (DNS etc)
  - Should not make browser hang if correct data is not available 
  - Asynchronous operation
    - Start fetch in background.
    - Wait for results, update.
  - How ? (A lot of the power of javascript comes from answering this question.)
#### Async 
* Events and callbacks
* Promises 
* fetch API
* axios

* ##### Callbacks
  - Function `doSomething` takes a long time to execute
  - `let result = doSomething()`
    - entire JS interpreter blocks till result is obtained (10^7 clock cycles till a result is obtained)
    - JS is a single threaded system - browser will hang
  - Instead start `doSomething()` and tell it to **call us back when done** 
* ###### Events
  - `button onclick` handler ? 
  - This is a function
    - But never explicitely called - not imperitive code
    - How to specify when to call
  - Event callback
    - Specify to DOM : on particular event, invoke function
* ###### JS : Event loops and call stacks
  - Call Stack
    - Execute all operations (function calls etc) in present scope in sequence
    - Go check "callback queue" to see if any new functions to be called 
      - if so execute them
      - keep checking ... events can be pushed to queue later by timeouts etc.
    - Reference material 
      - [Web API Event loops](https://html.spec.whatwg.org/multipage/webappapis.html#event-loops)
      - [How JavaScript works: Event loop and the rise of Async programming + 5 ways to better coding with async/await](https://blog.sessionstack.com/how-javascript-works-event-loop-and-the-rise-of-async-programming-5-ways-to-better-coding-with-2f077c4438b5)
      - [Concurrency model and the event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)

### Live session video
[Week 5 Live session on Monday 24th Jan 2022](https://www.youtube.com/watch?v=1AeOkI5CzSs)
