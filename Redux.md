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
## The core principles of Redux

**first principle**: `the Redux store is the single source of truth when it comes to application state`.
**second principle**: `state is read-only`.
**third principle**: `changes are made with pure functions`.


# Connect React to Redux
1. Configure Redux(in redux folder)
  * create actions folder, define actions
    ```js
    export default function addArticle (article) {
        return {
            type: 'ADD_ARTICLE',
            article
        }
    }
    ```
  * create reducer folder, define reducer
    ```js
    export default function articleReducer(state=[], action){
        switch(action.type){
            case 'ADD_ARTICLE':
                return [...state, {...action.course}]
            default:
                return state
        }
    }
    ```
  * create index.js, define root reducer
    ```js
    import { combineReducers } from 'redux';
    import articles from './articleReducer';


    const rootReducer = combineReducers({
      articles
    });

    export default rootReducer;
    ```
1. Configure React:
  * import provider in app or index.js
    ```js
    import React, { Component } from 'react';
    import {Provider} from 'react-redux';
    import configureStore from './redux/configureStore'
    import ArticlesPage from './components/ArticlesPage';

    const store = configureStore();

    class App extends Component {
      render() {
        return (
          <Provider store={store}>
            <ArticlesPage />
          </Provider>
        );
      }
    }

    export default App;
    ```
  * define component, import connect, define mapStateToProps, mapDispatchToProps
    ```js
    import React, { Component } from 'react';
    import { bindActionCreators } from 'redux';
    import {connect} from 'react-redux';
    import articleActions from '../redux/actions/articleActions'

    class ArticlesPage extends Component {
        state = {
            article: {
                title: ''
            }
        }

    handleChange = (e) => {
        const article = {...this.state.article, title: e.target.value}
        this.setState({ article })
    }

    handleSubmit = (e) => {
        e.preventDefault();
        this.props.actions(this.state.article)
        document.getElementById('newArticle').innerHTML = this.state.article.title
    }

      render() {
        return (
          <form onSubmit={this.handleSubmit}>
            <h2>Add article</h2>
            <input type="text" value={this.state.article.title} onChange={this.handleChange}/>
            <input type="submit" value="Add article"/>
            <div id="newArticle"></div>
          </form>
        );
      }
    }
    function mapStateToProps(state, ownProps) {
        return {
          article: state.article
        };
      }
      function mapDispatchToProps(dispatch) {
        return {
          actions: bindActionCreators(articleActions, dispatch)
        };
      }

    export default  connect(mapStateToProps, mapDispatchToProps)(ArticlesPage)
    ```

There is a method called **createStore()** on the Redux object, which you use to create the **Redux store**. This method takes a **reducer function** as a required argument. The reducer function simply takes state as an argument and returns state.



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
