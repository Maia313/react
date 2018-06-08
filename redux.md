
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
Since Redux is a state management framework, updating state is one of its core tasks. In **Redux**, all state updates are triggered by dispatching actions. An action is simply a JavaScript object that contains information about an action event that has occurred. The **Redux store** receives these action objects, then updates its state accordingly. Sometimes a Redux action also carries some data. For example, the action carries a username after a user logs in. While the data is optional, actions must carry a type property that specifies the 'type' of action that occurred.

Think of Redux actions as messengers that deliver information about events happening in your app to the Redux store. The store then conducts the business of updating state based on the action that occurred.

##### Define an Action Creator

After creating an action, the next step is sending the action to the Redux store so it can update its state. In Redux, you define action creators to accomplish this. An action creator is simply a JavaScript function that returns an action. In other words, action creators create objects that represent action events.

