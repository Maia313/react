# Patterns in React
> Some examples of patterns to use in React

* [# Conditional Rendering](#conditional-rendering)
* [# Rendering multiple components](#rendering-multiple-components)
* [# Composition](#composition)

### Conditional rendering

#### Traditional `if`

```jsx
export default function ToggleDiv({ visible }){
  if(visible){
    return <div> See me! </div>;
  }
  return '';
}
```

#### Ternary Operator

```jsx
export default function ToggleDiv({ visible }){
  let div = visible ? <div> See me! </div> : '';
  return(
    { div }
  );
}
```

_embedded ternary operator_
```jsx
export default function ToggleDiv({ visible }){
  return(
    { visible ? <div> See me! </div> : '' }
  );
}
```

#### `&&` Operator

```jsx
export default function ToggleDiv({ visible }){
  return(
    { visible && <div> See me! </div> }
  );
}
```
>It works because in JavaScript, `true && expression` always evaluates to `expression`, and `false && expression` always evaluates to `false`.
Therefore, if the condition is `true`, the element right after && will appear in the output. If it is `false`, React will ignore and skip it

* [Source: React Embedded Expressions](https://facebook.github.io/react/docs/introducing-jsx.html#embedding-expressions-in-jsx)

### Rendering multiple components

JavaScript has 3 very powerful array methods that can simplify rendering list of components [`map`, `filter` and `reduce`](https://danmartensen.svbtle.com/javascripts-map-reduce-and-filter)

An element created from an array need to have a **Key**:
>Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity

React documentation does not recommend using the index of the item from the array as a key but it can be used if we don't have a unique identifier. An item usually have some sort of `id` you can use. [Source @ react](https://facebook.github.io/react/docs/lists-and-keys.html#keys)

```jsx
export default function List({ arrayOfItems }) {
  const itemList = arrayOfItems.map( item =>
    <li key={ item.id }>{ item.name }</li>
  );
  return (
    <ul>
      { listItems }
    </ul>
  );
}
``` 
Every `<li>`-item could be its own component if it's a bigger component. You could also choose not to extract it to a component and create a _pseudo-component_ :

```jsx
export default function List({ arrayOfItems }) {
  
  const renderListItem = item => (
    <li key={ item.id }> { item.name } </li>
  );
  
  return (
    <ul>
      { arrayofItems.map(renderListItem) }
    </ul>
  );
}

```
[[Source]](https://hackernoon.com/10-react-mini-patterns-c1da92f068c5)

We could also do it like an embedded expression similiar to above:

```jsx
export default function List({ arrayOfItems }) {
  return (
    <ul>
      { arrayOfItems.map( item =>
          <li key={ item.id }>{ item.name }</li>
      )}
    </ul>
  );
}

```

### Composition

React gives us multiple ways to organize our components and sending them down the props-chain. Examples are mainly taken from this source:

* [React composition Cheat Sheet](https://github.com/xat/react-component-composition-cheatsheet)

```jsx
import Header from 'Navigation';
import React, { Component } from 'react';

class App extends Component {

  render(){
    <Layout>
      <Content />
    </Layout>
  }
}


const Layout = ({ children }) => (
  <div className="wrapper">
    <Header />
    <main className="container">
      { children }
    </main>
  </div>
);

const Content = () => (
  <div>Some fine content</div>
);

```
### Higher Order Component
> Takes another component as an argument and returns an enhanced component

```jsx
//Component without state, functional component
function Button(props){
  return <button onClick={props.onClick} > { props.toggle ? "On" : "Off" } </button>
}

//withToggleHOC, takes Component as argument and returns it with state and a toggle function
function withToggle(ComposedComponent){
  //Returns a new class with state and an onClick
  return class extends Component{
    state = {
      toggle: false
    }
    onClick = () => {
      this.setState({ toggle: !this.state.toggle});
    }
    //Render returns the passed component with new props from state and passing the previous props
    render(){
      return(
        <ComposedComponent {...this.props} toggle={this.state.toggle} onClick={this.onClick} />
      )
    }
  }
}


const ButtonWithToggle = withToggle(Button);
<ButtonWithToggle />
```
