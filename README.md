
### Core fundamentals:
1. `We think about and organize our React apps as components`
2. `Using JSX inside the render method` instead of React.createElement
3. `Data flows from parent component to children through props`
4. `Event flows from children to parent through functions`
5. `Utilizing React lifecycle methods`
6. `Stateful components and how state is different from props` 
7. `How to manipulate state while treating it as immutable`

**A handy framework for developing a React app from scratch**:
1. `Break the app into components`
2. `Build a static version of the app`
3. `Determine what should be stateful`
In order for our application to become interactive, we had to be able to modify the vote property on each product. Each product had to be mutable and therefore stateful.
4. `Determine in which component each piece of state should live`
ProductList managed the voting state using React component class methods.
5. `Hard-code initial state`
When we re-wrote ProductList to use this.state, we seeded it from Seed.products.
6. `Add inverse data flow`
We defined the handleUpVote function in ProductList and passed it down in props so that each Product could inform ProductList of up-vote events.
7. `Add server communication`
We did not add a server component to our last app, but we will be doing so in this one.

> fn(d) = V. Your UI is a function of your state and props are to components what arguments are to functions.
> Instead of your function taking in some arguments and returning a value, your function is going to take in some arguments  and return an object representation of your UI. 


### Curly braces, { } are used
  + `to access props`,
  + `to pass props`, 
  + `to access state`, 
  + `to insert comments into code`,
  + `to style components`.




