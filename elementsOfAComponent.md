
`Webpack's` core features: `module compilation` and the `ability to plug in loaders`.

### React.createElement() function accepts 3 arguments:
1. `The DOM element type`
2. `The element props`
3. `The children of the element`

### Stateless component

```js
var MyFirstComponent = function() {
          return React.createElement('div', null,
            React.createElement('h1', null, "This is my first component!")
          );
        };

        ReactDOM.render(
          React.createElement(MyFirstComponent),
          document.getElementById("app")
        );
```

**Props** --- **variables** that you pass **from the parent to the child** but the child cannot modify.

```js
var ce = React.createElement;

{/* child */}
var MyTitle = function (props) {
  return (
    ce('div', null,
      ce('h1', null, props.title)
    )
  );
};

{/* parent */}
var MyFirstComponent = function () {
  return (
    ce('div', null,
      ce(MyTitle, {title: 'House of Cards'}),
      ce(MyTitle, {title: 'Orange is the New Black'}),
      ce(MyTitle, {title: 'Stranger Things'})
    )
  );
};

ReactDOM.render(
  ce(MyFirstComponent),
  document.getElementById("app")
);
```
