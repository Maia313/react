
### Combine Multiple Reducers

When the state of your app begins to grow more complex, it may be tempting to divide state into multiple pieces. Instead, remember the first principle of Redux: `all app state is held in a single state object in the store`. Therefore, `Redux provides reducer composition as a solution for a complex state model`. You define multiple reducers to handle different pieces of your application's state, then compose these reducers together into one root reducer. The root reducer is then passed into the Redux `createStore()` method.

In order to let us combine multiple reducers together, Redux provides the `combineReducers()` method. This method accepts an object as an argument in which you define properties which associate keys to specific reducer functions. The name you give to the keys will be used by Redux as the name for the associated piece of state.

Typically, `it is a good practice to create a reducer for each piece of application state when they are distinct or unique in some way`. For example, in a note-taking app with user authentication, one reducer could handle authentication while another handles the text and notes that the user is submitting. For such an application, we might write the combineReducers() method like this:
```js
const rootReducer = Redux.combineReducers({
auth: authenticationReducer,
notes: notesReducer
});
```
Now, the key notes will contain all of the state associated with our notes and handled by our notesReducer. This is how multiple reducers can be composed to manage more complex application state. In this example, the state held in the Redux store would then be a single object containing auth and notes properties.

```js

// store custom implementation
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
```

### Define reducer without switch statement
```js
const ACTION_HANDLERS = {}

export default (state=initialState, action) {
  const HANDLER = ACTION_HANDLERS[action.type]
  
  return handler ? handler(state, action) : state;
}
```

```js
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';

const counterReducer = (state = 0, action) => {
  switch(action.type) {
    case INCREMENT:
      return state + 1;
    case DECREMENT:
      return state - 1;
    default:
      return state;
  }
};

const LOGIN = 'LOGIN';
const LOGOUT = 'LOGOUT';

const authReducer = (state = {authenticated: false}, action) => {
  switch(action.type) {
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

const rootReducer = Redux.combineReducers({
  count:counterReducer,
  auth:authReducer
})

const store = Redux.createStore(rootReducer);
```

### Send Action Data to the Store

By now you've learned how `to dispatch actions to the Redux store`, but so far these actions have not contained any information other than a type. You can also send specific data along with your actions. In fact, this is very common because actions usually originate from some user interaction and tend to carry some data with them. The Redux store often needs to know about this data.

```js
const ADD_NOTE = 'ADD_NOTE';

const notesReducer = (state = 'Initial State', action) => {
  switch(action.type) {
    // change code below this line
    case ADD_NOTE:
        return action.text;
    // change code above this line
    default:
      return state;
  }
};

const addNoteText = (note) => {
  // change code below this line
  const action = {
    type: ADD_NOTE,
    text: note
  }
  return action;
  // change code above this line
};

const store = Redux.createStore(notesReducer);

console.log(store.getState());
store.dispatch(addNoteText('Hello!'));
console.log(store.getState());
```
