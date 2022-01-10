## Week 3 Notes 

### Frontend Implementation 

* User Facing Part of an App
  - User Interface (UI) and User Experience (UX)
  - One of the most powerful User interfaces in existance is the Command Line (Terminal) 
    - Almost noone except a die hard Linux user is going to say it is good.
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
