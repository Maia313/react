# React

React uses a syntax extension of JavaScript called `JSX` that allows you to write HTML directly within JavaScript.

Because `JSX` is a syntactic extension of JavaScript, you can actually write JavaScript directly within `JSX`. To do this, you simply include the code you want to be treated as JavaScript within curly braces: `{ 'this is treated as JavaScript code' }`. Keep this in mind, since it's used in several future challenges.

`JSX` is compiled using Babel as a transpiler

**One important thing to know about nested JSX is that it must return a single element.**

This one parent element would wrap all of the other levels of nested elements.

Comments in JSX {/* */} 
```react
const JSX = (
  <div>
    <h1>Hello World</h1>
    <p>Lets render this to the DOM</p>
  </div>
);
```
