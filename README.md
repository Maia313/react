# React

1. `Render HTML elements to the DOM`
2. `Create components:2 ways`
3. `Parent-child relationship`

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


* Curly braces, { } are used
+ to accessing props,
+ to pass props, 
+ to access state, 
+ to insert comments into your code,
+ and style components.




