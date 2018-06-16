1. `Stateless functional components`
2. `Stateful components`
3. `this.setState`

#### Thinking in React
1. `Is it passed in from a parent via props? If so, it probably isn’t state.`
A lot of the data used in our child components are already listed in their parents. This criterion helps us de-duplicate.
For example, “timer properties” is listed multiple times. When we see the properties declared in EditableTimerList, we can consider it state. But when we see it elsewhere, it’s not.
2. `Does it change over time? If not, it probably isn’t state.`
This is a key criterion of stateful data: it changes.
3. `Can you compute it based on any other state or props in your component? If so, it’s not state.`
For simplicity, we want to strive to represent state with as few data points as possible.

When you want to aggregate data from multiple children or to have two child components communicate with each other, **move the state upwards** so that it lives in the parent component. The parent can then pass the state back down to the children via props, so that the child components are always in sync with each other and with the parent.

#### For each piece of state:
• Identify every component that renders something based on that state.
• Findacommonownercomponent(asinglecomponentaboveallthecomponents
that need the state in the hierarchy).
• Either the common owner or another component higher up in the hierarchy
should own the state.
• Ifyoucan’tfindacomponentwhereitmakessensetoownthestate,createanew
component simply for holding the state and add it somewhere in the hierarchy above the common owner component.


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
    
    this.setState({
      name: 'React Rocks!'
    });
    
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

You can use `state` in React applications in more complex ways than what you've seen so far. One example is to monitor the status of a value, then render the UI conditionally based on this value. There are several different ways to accomplish this, and here is one of them:

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      visibility: false
    };
    // change code below this line

    // change code above this line
  }
  // change code below this line

  // change code above this line
  render() {
    if (this.state.visibility) {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
          <h1>Now you see me!</h1>
        </div>
      );
    } else {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
        </div>
      );
    }
  }
};
```

**Description**

MyComponent has a visibility property which is initialized to false. 
The render method returns one view if the value of visibility is true, and a different view if it is false.

Currently, there is no way of updating the visibility property in the component's state. The value should toggle back and forth between true and false. 
There is a click handler on the button which triggers a class method called toggleVisibility(). 
Define this method so the state of visibility toggles to the opposite value when the method is called. If visibility is false, the method sets it to true, and vice versa.

Finally, click the button to see the conditional rendering of the component based on its state.

Hint: Don't forget to bind the this keyword to the method in the constructor!

**A simple counter**
```js
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
    this.reset = this.reset.bind(this);
    this.increment = this.increment.bind(this);
    this.decrement = this.decrement.bind(this);
  }

  reset() {
    this.setState({ count: 0 });
  }
  
  increment() {
    this.setState({ count: (this.state.count + 1) })
  }
  
  decrement() {
    this.setState({ count: this.state.count - 1 })
  }
  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};
```

**Handling forms**
```js
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
**Controlled form**

```js
class MyForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      input: '',
      submit: ''
    };
    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  handleChange(event) {
   // 
    this.setState({
      input: event.target.value
    });
  }
  handleSubmit(event) {
    // 
    event.preventDefault();
    this.setState({
      submit: this.state.input
    })
  }
  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          { /* change code below this line */ }
          <input value={this.state.input} onChange={this.handleChange} />
          { /* change code above this line */ }
          <button type='submit'>Submit!</button>
        </form>
      
        <h1>{this.state.submit}</h1>
      </div>
    );
  }
};
```
