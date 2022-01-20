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
    - in CSS 'responsive' is sometimes used to mean 'adaptive'

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
      - Flutter is a UI software development kit created by Google. It is used to develop cross platform applications. Dart is the programming language used to code Flutter apps.

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
  - Ephemeral - Lasting for a very short time (from flutter)

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
  - In actual frontends, you are trying to do something inbetween these

### Example : Tic - Tac - Toe
* What to display on the screen?
* Who determines the play?
* How should user input be collected and processed?



### Four different implementations of Tic - Tac - Toe
##### Source code: [Week 3 Code Base](https://gitlab.com/modern-application-development/mad2-xo)
___

#### Python Flask
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
* `BOARD` and `NEXT` indicate the complete state of the sysytem
  - By maintaining the state there is no smart functionality
  - Everything is maintained at the server
* Somebody else openng the page from another browser sees the game in progress

###### tic.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic-Tac-Toe</title>
  <style>
    .b {
      background-color: lightgrey;
    }
    .x .o {
      background-color: white;
    }
  </style>
</head>
<body>
  <h1>Next move: <img src="assets/{{['o','b','x'][next+1]}}.png"></h1>
  <table border="2px">
    {% for i in range(9) %}
      {% set r = i//3 %}
      {% set c = i%3 %}
      {% set e = board[i] %}
      {% set spclass = ['o','b','x'][e+1] %}
      {% if c == 0%}
    <tr>
      {% endif %}
      <td class="{{spclass}}">
        {% if e==0 %}
        <a href = "set/{{i}}">
        {% endif %}
        <img src="assets/{{spclass}}.png">
        {% if e==0 %}
        </a>
        {% endif %}
      </td>
      {% if c==2 %}
    </tr>
      {% endif %}
      {% endfor %}
  </table>
</body>
</html>
```

___

#### Javascript Implementation

###### tictactoe.js

```javascript
// Initialize, set up 
let board = [0, 0, 0, 0, 0, 0, 0, 0, 0];
let next  = 1;
let gState = 0;  // Game in progress

// Helper to convert number to character
function i2c(i)
{
    return i==1 ? 'x' : i==-1 ? 'o' : 'b';
}

function resetBoard() 
{
    board = [0, 0, 0, 0, 0, 0, 0, 0, 0];
    next  = 1;
    gState = 0;  // Game in progress
    updatePage();
}

// Update the page with present state of the board
function updatePage()
{
    const e = document.getElementById("next");
    if (gState == 0) {
        e.innerHTML = `<h1>Next move: <img src='assets/${i2c(next)}.png' /></h1>`;
    } else if (gState == 1) {
        e.innerHTML = `<h1>Yay! <img src='assets/x.png' /> won!</h1>`;
        e.innerHTML += `<button onclick='resetBoard();'>Play again?</button>`;
    } else if (gState == -1) {
        e.innerHTML = `<h1>Yay! <img src='assets/o.png' /> won!</h1>`;
        e.innerHTML += `<button onclick='resetBoard();'>Play again?</button>`;
    } else {
        e.innerHTML = `<h1>That was a boring draw!</h1>`;
        e.innerHTML += `<button onclick='resetBoard();'>Play again?</button>`;
    }
    
    for(const i in board) {
        const e = document.getElementById("td"+i);
        e.innerHTML = `<img src='assets/${i2c(board[i])}.png' onclick='updateEntry(${i});' />`;
    }
}

// Check state of play and update messages
function checkState()
{
    let patts = [[0,1,2], [3,4,5], [6,7,8], [0,3,6], [1,4,7], [2,5,8], [0,4,8], [2,4,6]];
    for (p of patts) {
        const sum = p.reduce((a, i) => a + board[i], 0);
        if (sum == 3) {
            return 1;   // X won
        } else if (sum == -3) {
            return -1;  // O won
        }
    }
    for (i in board) {
        if (board[i] == 0) return 0;    // Still in progress
    }
    return 2;   // Draw
}

// Update entry on click
function updateEntry(x)
{
    if (gState == 0 && board[x] == 0) {
        board[x] = next;
        next = -next;
        gState = checkState();
    }
    updatePage();
}

resetBoard();
```

###### index.html

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Tic-Tac-Toe</title>
        <style>
            .b {
                background-color: lightgrey;
            }
            .x .o {
                background-color: white;
            }
        </style>
    </head>
    <body>
        <span id="next"></span>
        <table border="2px">
            <tr>
                <td><span id="td0"></span></td>
                <td><span id="td1"></span></td>
                <td><span id="td2"></span></td>
            </tr>
            <tr>
                <td><span id="td3"></span></td>
                <td><span id="td4"></span></td>
                <td><span id="td5"></span></td>
            </tr>
            <tr>
                <td><span id="td6"></span></td>
                <td><span id="td7"></span></td>
                <td><span id="td8"></span></td>
            </tr>
        </table>
        <script src="./tictactoe.js"></script>
    </body>
</html>
```
___

#### Vue Implementation

###### index.html

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Tic-Tac-Toe</title>
        <style>
        </style>
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    </head>
    <body>
        <div id="app">
            <span v-html=headmsg></span>
            <table border="2px">
                <tr>
                    <td><tic v-bind:pos=0></tic></td>
                    <td><tic v-bind:pos=1></tic></td>
                    <td><tic v-bind:pos=2></tic></td>
                </tr>
                <tr>
                    <td><tic v-bind:pos=3></tic></td>
                    <td><tic v-bind:pos=4></tic></td>
                    <td><tic v-bind:pos=5></tic></td>
                </tr>
                <tr>
                    <td><tic v-bind:pos=6></tic></td>
                    <td><tic v-bind:pos=7></tic></td>
                    <td><tic v-bind:pos=8></tic></td>
                </tr>
            </table>        
        </div>
    <script src="./tictactoe-vue.js"></script>
    </body>
</html>
```

- `tic` tag is a component - a custom html tag - it has a custom property which is passed in as `props` 
- `v-html` is used to output formated html content into the `span` element

###### tictactoe-vue.js

```javascript
Vue.component('tic', {
    props: ['pos'],
    template: `<span v-html="imgl" v-on:click="setVal(pos);"></span>`,
    methods: {
        setVal() {
            this.$parent.setVal(this.pos);
        }
    },
    computed: {
        imgl: function() {
            return `<img src="assets/${this.$parent.v2c(this.$parent.board[this.pos])}.png" />`;
        }
    }
})

var app = new Vue({
    el: '#app',
    data: {
        board: [0, 0, 0, 0, 0, 0, 0, 0, 0],
        next: 1,
    },
    methods: {
        v2c(r) {
            return (r == 1) ? 'x' : (r == -1) ? 'o' : 'b';
        },
        setVal(i) {
            if (this.result == 0) {
                if (this.board[i] == 0) {
                    Vue.set(this.board, i, this.next);
                    this.next = -this.next;
                }
            }
        },
    },
    computed: {
        headmsg: function() {
            let msg = "";
            switch(this.result) {
                case 0: msg = `<h1>Next move: <img src="assets/${this.v2c(this.next)}.png" /></h1>`; break;
                case 1: msg = `<h1>Congratulations <img src="assets/x.png" />`; break;
                case -1: msg = `<h1>Congratulations <img src="assets/o.png" />`; break;
                case 2: msg = `<h1>Boring draw!</h1>`; break;
                default: msg = "Hello?"; break;
            }
            return msg;
        },
        result: function() {
            let patts = [[0,1,2], [3,4,5], [6,7,8], [0,3,6], [1,4,7], [2,5,8], [0,4,8], [2,4,6]];
            for (p of patts) {
                const sum = p.reduce((a, i) => a + this.board[i], 0);
                if (sum == 3) {
                    return 1;   // X won
                } else if (sum == -3) {
                    return -1;  // O won
                }
            }
            for (i in this.board) {
                if (this.board[i] == 0) return 0;    // Still in progress
            }
            return 2;   // Draw
        }
    }
})
```

- Line 16 : new vue app. Vue is a class 
- `el` associates it with the element that has id app
- Vue is looking for any changes in variables
  - any time a variable changes something needs to be updated
  - for arrays this is different
- Computed parameters `headmsg` and `result` are cached and only change when its dependent variables change 
- Vue does a dataflow analysis and figures out under what conditions `headmsg` should change
- Vue makes sure that the functions get called when required - this is where declarative programming comes into the picture

___


#### Alternate Vue Implementation without table, using CSS flex and Vue Components

###### index2.html

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Tic-Tac-Toe</title>
        <style>
            .board {
                display: flex;
                flex-wrap: wrap;
                width: 156px;
                height: 156px;
            }
            .cell {
                width: 48px;
                height: 48px;
                border: 2px solid;
                font-size: 36px;
                display: flex;
                align-items: center;
                justify-content: center;
            }
        </style>
        <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
    </head>
    <body>
        <div id="app">
            <board></board>
        </div>
    <script src="./ttt-comp-vue.js"></script>
    </body>
</html>
```

###### ttt-comp-vue.js

```javascript
Vue.component('tic', {
    props: ['val'],
    template: `<div @click="$emit('click')" class="cell"><span>{{val}}</span></div>`
})

Vue.component('board', {
    data: function() {
        return {
            board: [0, 0, 0, 0, 0, 0, 0, 0, 0],
            next: 1
        }
    },
    template: `
    <div class="boardtop">
        <span v-html="headmsg"></span>
        <div class="board">
            <div v-for="(n, i) in 9">
                <tic :val="v2c(board[i])" @click="update(i)"></tic>
            </div>
        </div>
    </div>
    `,
    methods: {
        v2c(r) {
            return (r == 1) ? 'X' : (r == -1) ? 'O' : '';
        },
        update(i) {
            if (this.result == 0) {
                if (this.board[i] == 0) {
                    Vue.set(this.board, i, this.next);
                    this.next = -this.next;
                }
            }
        }
    },
    computed: {
        headmsg: function() {
            let msg = "";
            switch(this.result) {
                case 0: msg = `<h1>Next move: ${this.v2c(this.next)}</h1>`; break;
                case 1: msg = `<h1>Congratulations X`; break;
                case -1: msg = `<h1>Congratulations O`; break;
                case 2: msg = `<h1>Boring draw!</h1>`; break;
                default: msg = "Hello?"; break;
            }
            return msg;
        },
        result: function() {
            let patts = [[0,1,2], [3,4,5], [6,7,8], [0,3,6], [1,4,7], [2,5,8], [0,4,8], [2,4,6]];
            for (p of patts) {
                const sum = p.reduce((a, i) => a + this.board[i], 0);
                if (sum == 3) {
                    return 1;   // X won
                } else if (sum == -3) {
                    return -1;  // O won
                }
            }
            for (i in this.board) {
                if (this.board[i] == 0) return 0;    // Still in progress
            }
            return 2;   // Draw
        }
    }
})

var app = new Vue({
    el: '#app',
})
```
* Some extra libraries on top of javascript
* Cleaner interface
* Elegance of vue comes when you start reusing components.
* chess.com is built using Vue.js.
* When the web was dealing only with documents, reactivity wasn't required
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

#### Two way binding for v-model in vue.js

* The v-model directive updates the template whenever the model changes and updates data model whenever the template changes.

##### Week 3 REPLIT
[Code With us - Asynchronicity in Javascript](https://replit.com/@constitution/MAD2Week3#script2.js)
