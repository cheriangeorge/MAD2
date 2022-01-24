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
    - Frontend implemented in browser, pulls data
* 

### Live session video
[Week 5 Live session on Monday 24th Jan 2022](https://www.youtube.com/watch?v=1AeOkI5CzSs)
