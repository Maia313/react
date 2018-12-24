## The core principles of Redux

```js
const createStore = (reducer, initialState) => {
  let currentState = initialState;
  const subscribeFns = [];
  
  return {
    getState: () => currentState,
    dispatch: action => {
      currentState = reducer(currentState, action);
      subscribeFns.forEach(cb => cb());  
    },
    subscribe: cb => {
      subscribeFns.push(cb);
    }
  }
}
}

1. `Create actions and action creators`, 
2. `Create a Redux store`, 
3. `Dispatch your actions against the store`,
4. `Design state updates with pure reducers`, 
5. `Manage complex state with reducer composition`,
6. `Handle asynchronous actions`. 

**Redux** is a state management framework that can be used with a number of different web technologies, including React.

In Redux, there is **a single state object that's responsible for the entire state of your application**. This means if you had a React app with ten components, and each component had its own local state, the entire state of your app would be defined by a single state object housed in the `Redux store`. This is the **first important principle to understand when learning Redux**: `the Redux store is the single source of truth when it comes to application state`.

The **Redux store** is an object which holds and manages application state. There is a method called **createStore()** on the Redux object, which you use to create the **Redux store**. This method takes a **reducer function** as a required argument. The reducer function simply takes state as an argument and returns state.

Declare a store variable and assign it to the **createStore()** method, passing in the **reducer** as an argument.
```js
const reducer = (state = 5) => {
  return state;
}

// Redux methods are available from a Redux object
// For example: Redux.createStore()
// Define the store here: 
let store = createStore(reducer);
```
Since Redux is a **state management framework**, `updating state` is one of **its core tasks**. In **Redux**, all state updates are triggered by dispatching actions. An action is simply a JavaScript object that contains information about an action event that has occurred. The **Redux store** receives these action objects, then updates its state accordingly. Sometimes a Redux action also carries some data. For example, the action carries a username after a user logs in. While the data is optional, actions must carry a type property that specifies the 'type' of action that occurred.

Think of Redux actions as messengers that deliver information about events happening in your app to the Redux store. The store then conducts the business of updating state based on the action that occurred.

### Define an Action Creator

After creating an action, the next step is sending the action to the Redux store so it can update its state. In Redux, you define action creators to accomplish this. An action creator is simply a JavaScript function that returns an action. In other words, action creators create objects that represent action events.

```js
const action = {
  type: 'LOGIN'
}
// Define an action creator here:
function actionCreator(){
  return action;
}
```

### Dispatch an Action Event

`dispatch` method is what you use to dispatch actions to the Redux store. Calling `store.dispatch()` and passing the value returned from an action creator sends an action back to the store.

Recall that action creators return an object with a type property that specifies the action that has occurred. Then the method dispatches an action object to the `Redux store`. Based on the previous challenge's example, the following lines are equivalent, and both dispatch the action of type LOGIN:
```js
store.dispatch(actionCreator());
store.dispatch({ type: 'LOGIN' });
```
```js
const store = Redux.createStore(
  (state = {login: false}) => state
);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};

// Dispatch the action here:
store.dispatch(loginAction());
```

### Handle an Action in the Store

After an action is created and dispatched, the Redux store needs to know how to respond to that action. This is the job of a reducer function. Reducers in Redux are responsible for the state modifications that take place in response to actions. A reducer takes state and action as arguments, and it always returns a new state. It is important to see that this is the only role of the reducer. It has no side effects — it never calls an API endpoint and it never has any hidden surprises. The reducer is simply a pure function that takes state and action, then returns new state.

Another key principle in Redux is that state is read-only. In other words, the reducer function must always return a new copy of state and never modify state directly. Redux does not enforce state immutability, however, you are responsible for enforcing it in the code of your reducer functions. You'll practice this in later challenges.

```js
const defaultState = {
  login: false
};

const reducer = (state = defaultState, action) => {
  // 
  if(action.type === 'LOGIN'){
    return {login: true};
  }
    return state;
  // 
};

const store = Redux.createStore(reducer);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};
```
### Use const for Action Types

A common practice when working with Redux is to assign action types as read-only constants, then reference these constants wherever they are used. You can refactor the code you're working with to write the action types as const declarations.

```js
const LOGIN = 'LOGIN';
const LOGOUT = 'LOGOUT';

const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => {

  switch (action.type) {

    case LOGIN:
      return {
        authenticated: true
      }

    case LOGOUT:
      return {
        authenticated: false
      }

    default:
      return state;

  }

};

const store = Redux.createStore(authReducer);

const loginUser = () => {
  return {
    type: LOGIN
  }
};

const logoutUser = () => {
  return {
    type: LOGOUT
  }
};
```
###  Register a Store Listener

Another method you have access to on the Redux store object is store.subscribe(). This allows you to subscribe listener functions to the store, which are called whenever an action is dispatched against the store. One simple use for this method is to subscribe a function to your store that simply logs a message every time an action is received and the store is updated.

```js
const ADD = 'ADD';

const reducer = (state = 0, action) => {
  switch(action.type) {
    case ADD:
      return state + 1;
    default:
      return state;
  }
};

const store = Redux.createStore(reducer);

// global count variable:
let count = 0;

function increment(){
  return count++;
}
store.subscribe(increment);
store.dispatch({type: ADD});
console.log(count);
store.dispatch({type: ADD});
console.log(count);
store.dispatch({type: ADD});
console.log(count);
```
