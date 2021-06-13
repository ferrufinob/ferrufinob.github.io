---
layout: post
title:      "React/Redux Application"
date:       2021-06-12 20:40:07 -0400
permalink:  react_redux_application
---


For the final project at Flatiron School, we were instructed to build an application utilizing Rails API as the backend and ReactJS/Redux as the front end. React has been fun to work with it comes with a useful component reusability feature, great dev tools, and easy-to-understand documentation.
One of my favorite websites is Pinterest, I could spend hours browsing, which inspired me to build my own Pinterest-like web application. While I do not have all of the amazing features Pinterest has, I am very happy with how my project turned out during my two-week build and plan on continuing to work on more features as my React knowledge expands(excited to get into React Hooks as we didn’t get to explore it during the curriculum).
One very important step that I made sure to not skip this time around was wireframing and planning all of my model associations. It helped greatly in deciding what containers, components, and routes would be needed.

<details>
<summary>Wireframe</summary>
![](https://miro.medium.com/max/1400/0*5fK1xENbalzF28vk)
</details>

Models:

- User: a user can log in, signup, and logout
- Pin: user can create and view pins
- Board: user can create and view boards



My application ended up having more components than I had originally planned. The state management library Redux was used to keep track and change state globally(it keeps track of everything in our app!). It was a bit tricky getting started with Redux but I broke everything in steps to help me:
React Redux Steps:

### Design the store: 
what kind of state do we need?
The store will be an object, a collection of different reducers and action creators

```
{
id: 1,
title: "
description: " 
}
```

### Define the action: 
what are some of the actions that a user can perform in our application? ex: delete or add something

```
{
 type: "ADD_PIN"
payload: {
      pins: ""
 }
}
```

## Create a reducer: 
a reducer is a pure function meaning that it will always return the exact same thing so be wary to not mutate state as we don’t want any side effects. A reducer takes 2 parameters: current state and the action

```
const initialState = {
boards: [],
loading: true,
};
const boardsReducer = (state = initialState, action) => {
switch (action.type) {
case "GET_BOARDS":
return { ...state, boards: action.payload, loading: false };
default:
return state;
 }
};
```

### Set up the store:

```
store.js
import {createStore} from redux
import reducer from './reducer'

const store = createStore(reducer)

export default store
```

### Dispatching actions: 
this is our action receiver. This function will persist changes to our state by calling our reducer.
```
connect(null, mapDispatchToProps)
// or destructor it
connect(null,{addPin})
```

Lastly! We need to ensure that our entire React application can access this data from the store. We do so by putting the <App> component inside the <Provider> component and then using connect() to specify which data we are listening for(mapStateToProps or mapToDispatch are the usual parameters) and which component we are providing that data to. To summarize Redux produces a centralized state.
Flatiron has been great and I will miss my amazing cohort lead and cohorts. It has been challenging to go from a complete beginner to where I am now, but my knowledge has grown(comparing my first ever project….).
