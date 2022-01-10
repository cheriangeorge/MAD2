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
  - Stateless protocols is useful when there are unreliable connections and devices
  - If there is stateful protocol this would become more complicated with too much overhead.
  - Maintianing state for too many people is not worth it . Look for alternative ways of maintianing state.
* How to convey state between client and server?
  - Client maintains state - sends requests to server for specific items
  - Server maintains state - only specific requests allowed to client
* In actual frontends you are trying to do something inbetween these

### Example : Tic - Tac - Toe
* What to display on the screen ?
* Who determines the play ?
* How should user input be collected and processed ?

___

### Four different implementations of Tic - Tac - Toe


### Python Flask
###### app.py
``` python
from flask import Flask, render_template,redirect
BOARD = [0] * 9 # 1 D representation of the Board
NEXT = 1        # 1 =X , -1 = O 

app = flask (__name__,
             static_folder='assets',
             template_folder = "templates")
@app.route('/')
def homepage():
  return render_template("tic.html",board=BOARD,next=NEXT)

def checkstate(board):
  patts = [(0,1,2),(3,4,5),(6,7,8),(0,3,6),(1,4,7),(2,5,8),(0,4,8),(2,4,6)]
  for p in patts:
    t = sum([board[x] for x in p])
    if (t==3):
      return 1 # X won
    elif (t==-3):
      return -1 # O won
  r = 0 
  for i in board:
    if i == 0:
      return 0 # Game still in progress
  return 2     # Draw
  

@app.route('/set/<int:i>')
def setvalue(i):
  global BOARD,NEXT
  BOARD[i] = NEXT
  NEXT = -NEXT
  r = checkstate(BOARD)
  if r == 0:
    return redirect('/')
  else: 
    return render_template("end.html",winner=r,board=BOARD,next=NEXT)

@app.route('/new')    
def newgame():
  global BOARD, NEXT
  BOARD = [0] * 9
  NEXT = 1
  return redirect('/')
  
app.run()
```
* BOARD and NEXT indicated the cmplete state of the sysytem
  - By maintaining the state there is no smart functionality
  - Everything is maintained at the server
* Somebody else openng the page from another browser sees the game in progress

###### tic.html

```html

```

___

### Javascript Implementation

```javascript
let board = [0,0,0,0,0,0,0,0,0];
let next = 1;
let gState = 0; // Game in progress

// Helper to convert number to character
function i2c(i)
```

___

### Vue Implementation

```html

```

- the `tic` tag is a component - a custom html tag - it has a custom property which is passed in as props 
- 

```javascript

```

- Line 16 : new vue app. Vue is a class 
- el associates it with the element that has id app
- vue is looking for any changes in variables (any time a variable changes something needs to be updated)
- for arrays this is different
- computed parameters headmsg and 
- vue does a dataflow analysis and figures out under what conditions headmsg should change
- vue makes sure that the functions get called when required - this is where declerative programming has come in to the picture

* Some extra libraries on top of javascript
* Cleaner interface
* Elegance of vue comes when you start reusing components.
* chess.com is built using vuejs.
* When the web was dealing only with documents, reactivity wasn't required
* 

___


### Alternate Vue Implementation without table, using css flex

```html

```

```javascript

```
___

### Screencast 3.1 Code
##### application.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello World</title>
    <!-- development version, includes helpful console warnings -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>
<body>
    <div id="app">
        <p>{{ message }}</p>
        Your Name : <input type="text" v-model="visitor_name"/>
        <p>Two way binding by v-model.</p>
        <p v-if="count == 0"> No replies yet </p>
        <p v-else-if="count > 5"> You are very popular</p>
        <p v-else>Number of repliess : {{ count }}</p>
        
        <button v-on:click="sayHi">Say Hi</button>
        <p>{{ visitor_name }} said hi.</p>
        <ul>
            <li v-for="name in visitors">{{ name }}</li>
        </ul>
    </div>

</body>
<script type="text/javascript" src="application.js"></script>
</html>
```

##### application.js

```javascript
//let message = "Hello World"

//document.getElementById("app").innerHTML = message ; 
var app = new Vue(
    {
        el : "#app",
        data : {
            message : "hello world",
            //count : 0,
            visitor_name : "",
            visitors : []
        },
        methods : {
            sayHi: function (){
                this.message = "Bye";
                //this.count +=1;
                this.visitors.push(this.visitor_name);
                this.visitor_name = "";
            }
        },
        computed : {
            count : function () {
                return this.visitors.length;
            }
        }
    }
)

```

##### Two way binding for v-model in vue.js

* The v-model directive updates the template whenever the model changes and updates data model whenever the template changes.
