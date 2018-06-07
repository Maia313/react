1. `Stateless functional components`
2. `Stateful components`
3. `this.setState`

### Stateless Functional Components

Except for the last challenge, you've been passing props to `stateless functional components`. These components `act like pure functions`. They `accept props as input and return the same view every time they are passed the same props`. 

`A stateless functional component` is any **function** you write which `accepts props` and `returns JSX`. `A stateless component`, on the other hand, is a **class** that `extends React.Component`, but does not use internal state (covered in the next challenge). Finally, `a stateful component` is any **component** that does **maintain its own internal state**. You may see stateful components referred to simply as components or React components.

### Stateful Components

`A common pattern is to try to minimize statefulness and to create stateless functional components wherever possible`. This helps contain your state management to a specific area of your application. In turn, this improves development and maintenance of your app by making it easier to follow how changes to state affect its behavior.

There is a component in the code that is trying to render a name property from its state. 
There is a state defined. The component is initialized with a state in the constructor and has a value assigned to it.

```js
class StatefulComponent extends React.Component {
  constructor(props) {
    super(props);
    //creates a stateful component
    this.state ={
      name:'React'
    }
  }
  render() {
    return (
      <div>
      //renders state in the user interface
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

Once you define a component's initial state, you can display any part of it in the UI that is rendered. If a component is `stateful`, it will always have access to the data in state in its render() method. You can access the data with `this.state`.

If you want to access a state value within the return of the render method, you have to enclose the value in curly braces.

State is one of the most powerful features of components in React. It allows you to track important data in your app and render a UI in response to changes in this data. If your data changes, your UI will change. React uses what is called a virtual DOM, to keep track of changes behind the scenes. `When state data updates, it triggers a re-render of the components using that data - including child components that received the data as a prop. React updates the actual DOM, but only where necessary.` This means you don't have to worry about changing the DOM. You simply declare what the UI should look like.

Note that if you make a component `stateful`, no other components are aware of its state. Its state is completely encapsulated, or local to that component, unless you pass state data to a child component as props. This notion of encapsulated state is very important because it allows you to write certain logic, then have that logic contained and isolated in one place in your code.

**Render State in the User Interface Another Way**

In the MyComponent render method a const called name is defined and it is equal to the name value in the component's state. Because you can write JavaScript directly in this part of the code, you don't have to enclose this reference in curly braces.

The return statement, renders this value in an h1 tag using the variable name. Remember, you need to use the JSX syntax (curly braces for JavaScript) in the return statement.

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    //
    this.state = {
      name: 'freeCodeCamp'
    }
  }
  render() {
    // 
    const name = this.state.name;
    // 
    return (
      <div>
       //
        <h1>{name}</h1>
       
      </div>
    );
  }
};
```

### Set State with `this.setState`

The previous challenges covered component state and how to initialize state in the constructor. 
There is also a way to change the component's state. React provides a method for updating component state called setState. 
You call the setState method within your component class like so: `this.setState()`, passing in an object with key-value pairs. 
The keys are your state properties and the values are the updated state data. For instance, if we were storing a username 
in state and wanted to update it, it would look like this:
```js
    this.setState({
    username: 'Lewis'
    });
```
React expects you to never modify state directly, instead always use `this.setState()` when state changes occur. 
Also, `you should note that React may batch multiple state updates in order to improve performance. 
What this means is that state updates through the setState method can be asynchronous.` 
There is an alternative syntax for the setState method which provides a way around this problem. 
This is rarely needed but it's good to keep it in mind! Please consult the React documentation for further details.

There is a button element in the code editor which has an onClick() handler. This handler is triggered when the button receives a click event in the browser, and runs the handleClick method defined on MyComponent. Within the handleClick method, update the component state `using this.setState()`. Set the name property in state to equal the string React Rocks!.

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      name: 'Initial State'
    };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    // change code below this line
    this.setState({
      name: 'React Rocks!'
    });
    // change code above this line
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```
### Use State to Toggle an Element

