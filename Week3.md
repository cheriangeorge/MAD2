## Week 3 Notes 

### Frontend Implementation 

* User Facing Part of an App
  - User Interface (UI) and User Experience (UX)
  - One of the most powerful User interfaces in existance is the Command Line (Terminal) 
    - Almost no one except a die hard Linux user is going to say it is good.
    - It is efficient and elegant
* Requirements
  - Avoid complex logic - Application logic should be in backend
  - No data storage
    - Application data is not stored in the frontend as far as possible (Suppose connection gets cut)
  - Work with stateless nature of HTTP
    - The messages that are exchanged between the client and the server ....
    - Remembering state is not part of the protocol
* Desirable 
  - Aesthetically pleaseing
  - Responsive - no lag / latency
  - Adaptive - different screens
    - in CSS responsive is sometimes used to mean adaptive

### Programming Styles

* Imperative - sequence of actions to achieve final result
  - Draw boxes for navigation, main text, fill in text, wait for clicks etc..
  - Functions for each step, composition of functions
* Declarative - specify desired result
  - Compiler / Interpreter knows how to achieve result
  - Function integration automated
* There are different types of problems where each style of programming style makes more sense.
 
### UI = f(state)
  - UI The layout of the screen
  - f = Your build methods
  - The application state. 
    - Once you have the application state you apply a set of functions on it and that results in what you see on the screen.
    - Credit : **Flutter** documentation "Start thinking declaritively"
      - A google framework based on the _____ black language

### State

* Internal details of the system : memory
* Reproducibility 
  - Given a "system state", the system should always respond the same way to input. 
* Complexity 
  - Any non-trivial application needs internal state. 

### System State

* Complete database of amazon.com , flipkart.com
  - Stocks of available items, prices, logged in / registered users etc.
* All news articles ever published on toi.com hindu.com bbc.com
* All students , courses, marks, certificates etc for NPTEL

* #### Typically huge but comprehensive
  - Completely independent of the user interface / frontend.

### Application State

* Application
  - System as seen by an individual user / session
  - Includes interactivity, session management
* Examples
  - Shopping cart, user preferences, theme
  - Followed news items , recommendations
  - Dashboard displays

### UI State (Ephemeral State)
* UI 
 - Part of application actually seen / interacted with
 - Ephemeral - Lasting for a very short time (From flutter)

* Examples :
  - Loading icons
  - Currently selected tab in multi-tab document / page

### Application and UI management
* HTTP is stateless
  - There are other protocols are stateful. The protocol itself maintains some extra information between the client and the server
* How to convey state between client and server?
  - Client maintains state - sends requests to server for specific items
  - Server maintains state - only specific requests allowed to client
* In actual frontends you are trying to do something inbetween these

### Example : Tic - Tac - Toe
* What to display on the screen ?
* Who determines the play ?
* How should user input be collected and processed ?




