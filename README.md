# React

1. `Render HTML elements to the DOM`
2. `Create components:2 ways`
3. `Parent-child relationship`
4. `Rendering JSX vs React components`
5. `Props`
6. `Pass an Array as Props`
7. `Recognize child parent components`
8. `Default props`
9. `Override default props`
10. `PropTypes`
11. `Access Props Using this.props`

React uses a syntax extension of JavaScript called `JSX` that allows you to write HTML directly within JavaScript.

Because `JSX` is a syntactic extension of JavaScript, you can actually write JavaScript directly within `JSX`. To do this, you simply include the code you want to be treated as JavaScript within curly braces: `{ 'this is treated as JavaScript code' }`. Keep this in mind, since it's used in several future challenges.

`JSX` is compiled using `Babel` as a transpiler

**One important thing to know about nested JSX is that it must return a single element.**

This one parent element would wrap all of the other levels of nested elements.

Comments in JSX {/* */} 
```js
const JSX = (
  <div>
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
);
```

### Render HTML elements to the DOM

So far, you've learned that `JSX` is a convenient tool to write readable HTML within JavaScript. With React, we can render this `JSX` directly to the HTML DOM using React's rendering API known as `ReactDOM`.

`ReactDOM` offers a simple method to render React elements to the DOM which looks like this: `ReactDOM.render(componentToRender, targetNode)`, where the first argument is the React element or component that you want to render, and the second argument is the DOM node that you want to render the component to.

As you would expect, `ReactDOM.render()` must be called after the JSX element declarations, just like how you must declare variables before using them.

### Create components

There are **two ways** to create a *React component*. **The first way** is to **use a JavaScript function**. *Defining a component in this way creates a stateless functional component.* The concept of state in an application will be covered in later challenges. For now, think of a stateless component as one that can receive data and render it, but does not manage or track changes to that data. (We'll cover the second way to create a React component in the next challenge.)

To create a component with a function, you simply write a JavaScript function that returns either `JSX` or `null`. One important thing to note is that React requires your function name to begin with a capital letter. Here's an example of a stateless functional component that assigns an HTML class in JSX:

```js
// After being transpiled, the <div> will have a CSS class of 'customClass'
const DemoComponent = function() {
return (
<div className='customClass' />
);
};
```

Because a `JSX` component represents HTML, you could put several components together to create a more complex HTML page. This is one of the key advantages of the component architecture React provides. It allows you to compose your UI from many separate, isolated components. This makes it easier to build and maintain complex user interfaces.

The **second way** to define a React component is with the **ES6 class syntax**. In the following example, Kitten extends `React.Component`:

```js
class Kitten extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <h1>Hi</h1>
    );
  }
}
```

This creates an ES6 class Kitten which extends the `React.Component` class. So the `Kitten` class now has access to many useful React features, such as local state and lifecycle hooks. Don't worry if you aren't familiar with these terms yet, they will be covered in greater detail in later challenges.

Also notice the Kitten class has a constructor defined within it that calls `super()`. It uses `super()` to call the constructor of the parent class, in this case `React.Component`. The constructor is a special method used during the initialization of objects that are created with the class keyword. `It is best practice to call a component's constructor with super, and pass props to both.` This makes sure the component is initialized properly. For now, know that it is standard for this code to be included. Soon you will see other uses for the constructor as well as props.

### Parent-child relationship

Now we will look at how we can compose multiple React components together. Imagine you are building an App and have created three components, a Navbar, Dashboard, and Footer.

To compose these components together, you could create an App parent component which renders each of these three components as children. To render a component as a child in a React component, you include the component name written as a custom HTML tag in the JSX. For example, in the render method you could write:

```js
return (
<App>
<Navbar />
<Dashboard />
<Footer />
</App>
)
```

When React encounters a custom HTML tag that references another component (a component name wrapped in `< />` like in this example), it renders the markup for that component in the location of the tag. This should illustrate the `parent/child` relationship between the `App` component and the `Navbar`, `Dashboard`, `and Footer`.

```js
const ChildComponent = () => {
  return (
    <div>
      <p>I am the child</p>
    </div>
  );
};

class ParentComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>I am the parent</h1> 
          <ChildComponent />
      </div>
    );
  }
};
```

### Rendering JSX vs React components

* JSX .....................ReactDOM.render(componentToRender, targetNode)
* React components ........ReactDOM.render(<ComponentToRender />, targetNode)

### Props

Another feature very common in React: `props`. `In React, you can pass props, or properties, to child components`. Say you have an App component which renders a child component called Welcome that is a stateless functional component. You can pass Welcome a user property by writing:

```js
<App>
<Welcome user='Mark' />
</App>
```

You use custom HTML attributes that React provides support for to pass the property user to the component Welcome. Since Welcome is a stateless functional component, it has access to this value like so:

```js
const Welcome = (props) => <h1>Hello, {props.user}!</h1>
```
It is standard to call this value `props` and when dealing with stateless functional components, you basically consider it as an argument to a function which returns `JSX`. You can access the value of the argument in the function body. With class components, you will see this is a little different.

### Pass an Array as Props

The last challenge demonstrated how to pass information from a parent component to a child component as props or properties. This challenge looks at how arrays can be passed as props. To pass an array to a JSX element, it must be treated as JavaScript and wrapped in curly braces.

```js
<ParentComponent>
<ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>
```

The child component then has access to the array property colors. Array methods such as join() can be used when accessing the property.
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

React also has an option to set `default props`. You can assign default props to a component as a property on the component itself and React assigns the default prop if necessary. This allows you to specify what a prop value should be if no value is explicitly provided. For example, if you declare `MyComponent.defaultProps = { location: 'San Francisco' }`, you have defined a location prop that's set to the string San Francisco, unless you specify otherwise. React assigns default props if props are `undefined`, but if you pass `null` as the value for a prop, it will remain `null`.

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

You can set **propTypes** on your component to require the data to be of type array. This will throw a useful warning when the data is of any other type.

It's considered a best practice to set **propTypes** when you know the type of a prop ahead of time. You can define a **propTypes** property for a component in the same way you defined **defaultProps**. Doing this will check that props of a given key are present with a given type. Here's an example to require the type function for a **prop** called **handleClick**:

```js
MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }
```
In the example above, the `PropTypes.func` part checks that **handleClick** is a function. Adding **isRequired** tells React that **handleClick** is a required property for that component. You will see a warning if that prop isn't provided. Also notice that func represents function. `Among the seven JavaScript primitive types, function and boolean (written as bool) are the only two that use unusual spelling.` In addition to the primitive types, there are other types available. For example, you can check that a prop is a React element.

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

The last several challenges covered the basic ways to pass `props` to child components. But what if the child component that you're passing a prop to is an `ES6 class component`, rather than a `stateless functional component`? The ES6 class component uses a slightly different convention to access props.

Anytime you refer to a class component within itself, you use the `this` keyword. To access props within a class component, you preface the code that you use to access it with this. `For example, if an ES6 class component has a prop called data, you write {this.props.data} in JSX.`

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

