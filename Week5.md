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
* ##### Events
  - `button onclick` handler ? 
  - This is a function
    - But never explicitely called - not imperitive code
    - How to specify when to call
  - Event callback
    - Specify to DOM : on particular event, invoke function
* ##### JS : Event loops and call stacks
  - Call Stack
    - Execute all operations (function calls etc) in present scope in sequence
    - Go check "callback queue" to see if any new functions to be called 
      - if so execute them
      - keep checking ... events can be pushed to queue later by timeouts etc.
    - Reference material 
      - [Web API Event loops](https://html.spec.whatwg.org/multipage/webappapis.html#event-loops)
      - [How JavaScript works: Event loop and the rise of Async programming + 5 ways to better coding with async/await](https://blog.sessionstack.com/how-javascript-works-event-loop-and-the-rise-of-async-programming-5-ways-to-better-coding-with-2f077c4438b5)
          - how `setTimeout` works with the call stack
      - [Concurrency model and the event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
          - **'Run to completion' once the program enters the call stack** - Nothing else can come and run on the call stack. Nothing can stop it and run in another thread. It can stay over there and block your program. Be carefult about having things that terminate quickly.

* ##### Callbacks
  - Higher order function call other functions depending on some conditions
  - Example
      ```javascript
      doSomething (successCB,failureCB) {
        let result = doLongComputation();
        if (result) successCB(); //called as function
        else failureCB();
      }
      
      ```
* ##### Promises : alternative syntax ?
  - `doSomething().then(successCB,failureCB);`
  - [Mozilla Using Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
    - More than just syntax
      - additional guarantees on behaiviour
      - easier chaining

* ##### Concurrency and Parallelism
  - Concurrent: multiple operations can be in process at the same time 
    - But maybe they only execute in time-multiplexed manner and not literally at the same time instant
    - More important from the POV of the user.
  - Parallel : multiple concurrent operations are actually physically executing at the same time 
    - Can happen only if you have multiple processors present.
  - Parallel requires concurrent; not vice-versa
  - Async operations bring in a notion of concurrency - whether this is actually implemented in parallel or time multiplexed is up to run time 
  - Web workers, timers - parallel execution. 
* ##### Async op : fetch
  - Fetching a URL must be async
    - no guarantee on network speeds
    - Server load may result in slow responses
    - Broken connection or other network failures can happen 
  - JS API since ES6 : `fetch()`
    - implemented using `Promise`
    - Built into most browsers - "Polyfills" available for backward compatibility.
  - [Mozilla Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) 
* ##### Axios
  - Custom API library with smilar functionality to fetch
    - can be used on most browsers - provides good backward compatibility
    - also works on nodejs
  - [Axios or Fetch API](https://blog.logrocket.com/axios-or-fetch-api/)

#### Existing APIs we can use

* ##### Building a frontend 
  - Many public and useful APIs already exist
  - Significant development possible with just API access
  - Examples:
    - [GitHub APIs](https://api.github.com/)
    - [Mediawiki APIs](https://www.mediawiki.org/wiki/API:Main_page)
    - [Open Weather Map](https://openweathermap.org/api)
      - `curl 'api.openweathermap.org/data/2.5/weather?q=chennai&appid=524e66603815fe9f71171c6c7fde1e86'`
    - [Hackernews](https://hacker-news.firebaseio.com/v0/item/8863.json?print=pretty)
##### Code Example
  - index1.html
  ```html
  cc
  ```
  - weather1.js
  ```javascript
  cc
  ```
  - weather.js
  ```javascript
  cc
  ```

### Live session video
[Week 5 Live session on Monday 24th Jan 2022](https://www.youtube.com/watch?v=1AeOkI5CzSs)

### Screen cast REPLIT link
[REPLIT Screencast](https://replit.com/@constitution/MAD2Week5Screencasts)
