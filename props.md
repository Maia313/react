### Props

1. `Rendering JSX vs React components`
2. `Props`
3. `Pass an Array as Props`
4. `Recognize child parent components`
5. `Default props`
6. `Override default props`
7. `PropTypes`
8. `Access Props Using this.props`

### Rendering JSX vs React components

* JSX .....................ReactDOM.render(componentToRender, targetNode)
* React components ........ReactDOM.render(<ComponentToRender />, targetNode)

### Props

Another feature very common in React: `props`. `In React, you can pass props, or properties, to child components`. 
Say you have an App component which renders a child component called Welcome that is a stateless functional component. 
You can pass Welcome a user property by writing:

```js
<App>
<Welcome user='Mark' />
</App>
```

You use custom HTML attributes that React provides support for to pass the property user to the component Welcome. 
Since Welcome is a stateless functional component, it has access to this value like so:

```js
const Welcome = (props) => <h1>Hello, {props.user}!</h1>
```
It is standard to call this value `props` and when dealing with stateless functional components, you basically consider 
it as an argument to a function which returns `JSX`. You can access the value of the argument in the function body. 
With class components, you will see this is a little different.

### Pass an Array as Props

The last challenge demonstrated how to pass information from a parent component to a child component as props or properties. 
This challenge looks at how arrays can be passed as props. To pass an array to a JSX element, it must be treated as 
JavaScript and wrapped in curly braces.

```js
<ParentComponent>
<ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>
```

The child component then has access to the array property colors. Array methods such as join() can be used when accessing 
the property.
```js
const ChildComponent = (props) => <p>{props.colors.join(', ')}</p>
```
This will join all colors array items into a comma separated string and produce:
```js
<p>green, blue, red</p>
```
Later, we will learn about other common methods to render arrays of data in React.

### Recognize child parent components
```js
const ChildComponent = (props) => <p>{props.colors.join(', ')}</p>
```
```js
<ParentComponent>
<ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>
```

```js
const List= (props) => {
  { /* change code below this line */ }
  return <p>{}</p>
  { /* change code above this line */ }
};

class ToDo extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>To Do Lists</h1>
        <h2>Today</h2>
        { /* change code below this line */ }
        <List/>
        <h2>Tomorrow</h2>
        <List/>
        { /* change code above this line */ }
      </div>
    );
  }
};
```

### Default props

React also has an option to set `default props`. You can assign default props to a component as a property on the 
component itself and React assigns the default prop if necessary. This allows you to specify what a prop value should be if
no value is explicitly provided. For example, if you declare `MyComponent.defaultProps = { location: 'San Francisco' }`, 
you have defined a location prop that's set to the string San Francisco, unless you specify otherwise. 
React assigns default props if props are `undefined`, but if you pass `null` as the value for a prop, it will remain `null`.

### Override default props
```js
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}

Items.defaultProps = {
  quantity: 0
}

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items quantity={10} />
  }
};
```

### PropTypes

You can set **propTypes** on your component to require the data to be of type array. This will throw a useful warning when 
the data is of any other type.

It's considered a best practice to set **propTypes** when you know the type of a prop ahead of time. You can define 
a **propTypes** property for a component in the same way you defined **defaultProps**. Doing this will check that props of 
a given key are present with a given type. Here's an example to require the type function 
for a **prop** called **handleClick**:

```js
MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }
```
In the example above, the `PropTypes.func` part checks that **handleClick** is a function. Adding **isRequired** tells 
React that **handleClick** is a required property for that component. You will see a warning if that prop isn't provided. 
Also notice that func represents function. `Among the seven JavaScript primitive types, function and boolean (written as bool)
are the only two that use unusual spelling.` In addition to the primitive types, there are other types available. 
For example, you can check that a prop is a React element.

**Note**: As of React v15.5.0, `PropTypes` is imported independently from React, like this:

```js
import React, { PropTypes } from 'react';
```


```js
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
};

Items.propTypes = {
  quantity:PropTypes.number.isRequired 
}

Items.defaultProps = {
  quantity: 0
};

class ShoppingCart extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return <Items />
  }
};
```

### Access Props Using this.props

The last several challenges covered the basic ways to pass `props` to child components. But what if the child component 
that you're passing a prop to is an `ES6 class component`, rather than a `stateless functional component`? 
The ES6 class component uses a slightly different convention to access props.

Anytime you refer to a class component within itself, you use the `this` keyword. To access props within a class component, 
you preface the code that you use to access it with this. `For example, if an ES6 class component has a prop called data, 
you write {this.props.data} in JSX.`

```js
class ReturnTempPassword extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
         
            <p>Your temporary password is: <strong>{this.props.tempPassword}</strong></p>
            
        </div>
    );
  }
};

class ResetPassword extends React.Component {
  constructor(props) {
    super(props);

  }
  render() {
    return (
        <div>
          <h2>Reset Password</h2>
          <h3>We have generated a new temporary password for you.</h3>
          <h3>Please reset this password from your account settings ASAP.</h3>
          
          <ReturnTempPassword tempPassword='tempPassword' />
          
        </div>
    );
  }
};
```
