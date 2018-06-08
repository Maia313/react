
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

